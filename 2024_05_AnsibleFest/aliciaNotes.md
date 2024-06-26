# AnsibleFest 2024 through Alicia's eyes

I had three main areas of interest for AnsibleFest 2024: firewall automation, VMware automation, and ServiceNow automation. I also learned some things about security tools.

## Automating firewalls

A theme of several presentations I went to was "start small, think big." For firewall automation, the transition to infrastructure as code is going to be big, but we can create smaller milestones like a read-only playbook (we've already started this), and a small read-write use case.

We can trigger Tower runs based on merged PRs on GitHub, this may be useful for our firewall workflow.

We can (and maybe should) put the network EE on a separate execution node. We can even put that node in a different subnet / behind the firewall.

### Automating Pan-OS workshop

Can do this workshop (and several others) any time at http://red.ht/ansible-labs. The lab uses a single playbook for at least two templates, using tags in the templates to control which actions run and which are skipped.

There is a pre-built EE for Pan-OS: registry.gitlab.com/redhatautomation/panos-ee:latest.

There are complications to automating Pan-OS.


The PanOS demo does commit as a separate template. I think this was the combined "commit and pushto devices", but it might not have gone through Panorama at all.

Network modules support check mode ("dry run"). They also support dynamic inventory. You can check the collections inside an EE using inventory. I think this is from github.com/network-automation/panos-instruqt.

Some of the templates in the lab launch directly from the list with no review/confirm screen - not sure how to do that.



### Discover Financial Services preso

Discover uses YAML data structures as variables, taking steps to improve a brownfield network setup. They have designed "undo" templates that re-use variables in case something goes wrong. They integrate with SNow and Ansible for their network automation.

Their workflow begins with a PR that updates the data structure. Then they have a pre-change validation step. If that fails (usually because the requested change is not allowed), they have a "handle failure" template, which passes messages to the requester but allows the overall workflow to "succeed" so the automation team doesn't need to review every bad request from a user. They also have a post-change validation step. If that fails, the "handle failure" template also runs, kicking off a Back Out This Change playbook that uses `set_stats` for tracking the change that needs to be reverted. The "handle failure" template also uses some vars and tasks that were new to me:  `ansible_failed_task.name` and `meta: end_play`, which ends the play cleanly.

They use Tower workflows to ensure that they don't have parallel changes or race conditions. They cache a copy of the current firewall config, pulling the data once a day and running their playbooks against that instead of against the live firewall. Once a day all approved changes go in together from Tower, so they are not constantly updating the firewall.

They use GitHub status checks and Tower vars like `workflow_stage` and `workflow_stage_complete` to provide feedback to users at every stage of the change process.
They have used a "Tiger Team" approach to major changes, where everyone on the team sets aside all other work for a week to focus on a major project.

This was a brownfield project - their existing firewall objects do not all have ownership tags, so they couldn't export their data and start from scratch. However, the automation made a migration go quickly, and they are working on consistent naming and visibility. Their goal is to develop a source of truth with full data (ownership, etc.). They do have a snapshot of the data before each change which they compare to the data after the change. They do not remove rules.

### TDBank - Network Automation at Scale

TDBank's Source of Truth is variables. Their goal in developing network automation was Streamlined, Secure, and Stable.

They learned that they needed to understand everyone's risk tolerance as they automated the network. They changed their culture through empowerment.

Could we use EDA to add bad bots to our banlist automatically?
Could PRs against the inventory dir in princeton_ansible kick off network automation runs?

## Automating VMware

Look for a read-only use case. The simplest might be to report on how many running VMs we have per host. Next most complicated would be to pull a list of all running VMs with a bunch of info about them. Could we compare this list to our inventory, or even implement dynamic inventory with VMware? We can probably have dynamic inventory side-by-side with our repo-based inventory. Also, EDA uses plugins and has ones that connect to all the major cloud providers (check if VMware is one of them).

Podman Desktop can now build bootable images. Can we create our ISOs for VMware this way?

## Automating ServiceNow

The developer who maintains the servicenow.itsm collection told me that ServiceNow has a Developer Program, and if you sign up for it you get a dev/test instance of SNow. That's how they test changes to the collection. I will sign up for one of these to test our first attempts at automating SNow connections.

He also suggested that we could bypass the need for a service login if we collection individual credentials in the playbook. We can use a Survey in any Templates that connect to ServiceNow and pass the credentials that way instead of storing them in Tower. Check if we can have invisible/secret survey responses - we don't want our passwords visible in Tower.

ServiceNow offers a plugin and API for Ansible now. You get this from the ServiceNow store. I'm not sure what functionality the plugin and API offer vs. what the servicenow.itsm collection offers.

## Security

Need to think about the fact that VMs in the same data center pass traffic to each other without hitting the firewall at all.

### EDA and CrowdStrike (DevZone)

There is a supported crowdstrike collection. Can we use that to install Falcon instead of the command module? Falcon integrates with Slack and SNow and Tower to leverage EDA for remediation. The data comes from the Falcon global customer data and includes threat actor profiles. Aim is to remediate in under 60 minutes to prevent lateral moves by the threat actors. The rulebook in the demo changed network rules to isolate the compromised box. Could we do that at PU/PUL?

The crowdstrike/falcon collection does inventory management and would allow us to find any machines on a given subnet that do not have Falcon installed. This would be more comprehensive than using BigFix.

### Policy as Code with Ansible (DevZone)

We can create rules in Tower as policy books - things like "you can't run during a maintenance window / peak usage hours" or "your Tower project must be signed /" or "passwords must be N characters long". You could use `assert` to define rules but it does not offer enforcement - policy books will soon offer enforcement. See redhat.com/PoC for updates.
