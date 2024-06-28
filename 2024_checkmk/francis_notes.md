# Keynote

* CheckMK raw edition is `nagios` based and the paid version is a proprietary one that will be more performant than the `raw_edition`
* CheckMK Inc (US Based LLC) v/s CheckMK service providers
  * not clear what (if any?) the distinction is
* Use of labels on Cloud based hosts
  * uses the [push model](https://checkmk.com/werk/15244)
* CheckMK is new in the application monitoring environment
  * Creating OpenTelemetry in CheckMK
  * Synthetic monitoring presentation today.
    * [RobotMK](https://github.com/elabit/robotmk)
  * Who is Simon(?) and Synthetic monitoring. Is this available on the `raw_edition`
  * New Agent API used for building extensions
  * Ansible Collection
    * First Class citizen in the ecosystem
    * Committed to supporting integration

## Sessions 1 - 2

### CheckMK 2.3 at a Glance

* CheckMK MSP has segregation
* ripped out check_http nagios and rewrote it to run
  * no longer dependent on curl
  * look at Services for HTTP
  * this is present today and worth further exploration
  * can use http2 and can use token based auth
* CheckMK how to migrate
  * What will break on the migration
  * Read the [Documentation](https://docs.checkmk.com/latest/en/update_major.html)
  * Worthwhile exercise for 2.4
* CheckMK DB monitoring
  * uses SQL in general. Started with MsSQL and then generalized
  * detect is there a databases
  * Can you connect to local and remote
    * timeout and caching
  * Plugin does SQL execution
    * written in rust
    * the rcc binary
* CheckMK K8s monitoring
* CheckMK Storage monitoring
  * can monitor Purity API
  * linux bonding extended improved
* CheckMK Alerts
  * Dash List (top consumer of resources)
  * CheckMK predicted monitoring
  * CheckMK network visualization at L2 level
    * thl-cmk (search on the CMK exchange)

### Modifications of UI over the years

* Definition of "sticky" in the acknowledgements
  * Sticky stays the same until it goes to OK
  * Sticky has a date and time picker
* Is there a way to automate "downtime" via a playbook
* Who is activating changes
* We can revert changes (some changes do not require activation)
  * it shows what rules you will revert
* Filters also include folders in the Setup
* Navigate CheckMK using the keyboard
* Our extensions should work with CheckMK
  * CheckMK Plugins are now covered also
    * Read up on [plugins changes](https://checkmk.com/werk/16259)
* CheckMK Pre-Flight Check (see upgrade) is now reversible

## Session 3

## Session 4 - 7

### Synthetic Monitoring

* Is something in the UI broken
* Synthetic is written in rust :smile:
* Usable to non [software developers](https://checkmk.com/product/synthetic-monitoring)
  * Uses the [RobotMK](https://github.com/elabit/robotmk)
  * Fuller [Documentation](https://www.robotmk.org/en/)
* Test [CheckMK](https://play.checkmk.com)

### CheckMK for DevOps (Jenkins)

* OpenSource (they evaluated it)
* Adapt and Enhance

## Session 8 - 9

### Cloud Monitoring Made Simple

* what is AWS-dcd connector
  * this depends on existence of a test-connection
* 2.4 simplifies AWS significantly
  * Most of the funtionality already exists
  * Working with UI/UX team on this

### CheckMK 2.4 Monitoring

* We can create a "hard state" with one click
* New button called "Test Notifications"
  * will simulate events to test
  * Simulation has multiple options
  * includes plugins output
  * Advanced condition simulation

### CheckMK 2.4 Roadmap

#### Guiding Principles

* No feature is built without user input/involvement
* 4 year plan (include support tickets)
* Remain transparent about roadmap and progress

#### CheckMK 2.4

* Full hybrid infrastructure
  * Network device monitoring via SNMP
* Certified Exchange Store
* Application Monitoring
  * this is not APM
* Prometheus and OpenTelemetry
  * agent will be able to collect OTEL data
* New Timeseries backends for short-lived data (not likely in 2.4)
* Training models on CheckMK documentation
* Adding distributed data via dynamic piggyback
* FIPS Compliance
* Baseboard management controller
  * Out-of-band management
* Will be review PRs with the reduction of the backlog
* Configuration Changes
  * reduction of configuration errors.
  * multi-step workflows.
  * protect important rules (do NOT delete the automation user)
* REST-API performance improvements
* Language Support improvements
* Navigation (For 2.5)
  * Balance rate of change v/s improvements

### Pre Questions

* Can we skip service discovery, or only run it on certain machines? We have a lot of unused services on our machines, and we can monitor the important ones with our Rails Status pages.
* Can one server “live” in more than one folder? We have servers that we would like to alert, say, both Ops and DLS
  * Yes this is possible using the [Clustering](https://docs.checkmk.com/latest/en/clustered_services.html)
  * Also Overlapping Clustering
* How do we manage monitoring for VMs if we install both the agent and vSphere monitoring/piggyback? What are the advantages/disadvantages of doing one, the other, or both?
* Can we modify checks that are built in?  Aka can we tell the system we do not entirely care about our EC2 limits
* How do we reduce notifications for things that affect multiple machines? For example, we mount diglibdata on all our Solr machines, but we really only need one notification when it gets too full. And again, how do we represent this in Ansible?
* How do we automate changing the threshold for a full disk warning for a specific machine or group of machines? For example, we might want to warn about the Isilon at 85% instead of at 80%, since it is so large - how do we represent this as a variable so we can rebuild the check with Ansible?
  * You can use the Magic Factor
  * Search for Magically in the documentation
* How do we get Slack notifications to use Slack usernames instead of CheckMK usernames (which are NetIDs) when "@"-ing on Slack? Ideally we would use team names for most Slack notifications, so people can go on vacation without worrying that notifications will go unnoticed. I’m guessing this is something to do with editing Contact Groups to include Slack info? or Notification rules?
  * Not really

#### New Points received

* Instana
* Datadog Intergration is there today
* CPU Load has an editable defaults page (as of 2.3) WAT!!
* Magic Factor
* It is possible to monitor log files in [CheckMK](https://checkmk.com/videos/en/ep-22-monitoring-logfiles-checkmk). Use case defined was checking if a Windows Server was gracelessly shutdown. This is possible on `raw_edition`
