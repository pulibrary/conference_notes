### Accessible Terminal Application for Screen Reader Users by Takahiro Miura and Junji Onishi 

* [research paper related to this presentation](https://csun.at/draftvol12) (pages 185-197)
* Background
  * IDEs are becoming increasingly complex, presenting additional accessibility challenges
  * [Grid-coding style is one approach](https://pure.psu.edu/en/publications/grid-coding-an-accessible-efficient-and-structured-coding-paradig)
* WEBBY Term is their terminal
  * It keeps the last output of STDOUT saved temporarily so that users can easily review in a complementary window
  * Notification with sound effect when the execution of the command completes, so that you know it's time to review the output
  * screen scrolling functionality
* They tested with blind and low vision computer science students
  * most used NVDA, 2 used PC-Talker (Japanese screen reader), 1 used JAWS
  * the test included switching between the terminal task and other web browser tasks (e.g. start `git clone` in the terminal, go search something unrelated, and go back to `ls` the cloned repository when it was done)
  * Tasks were done on both PowerShell in WEBBY Term
* Feedback:
  * Powershell presents challenges in navigation, checking details without redirecting STDOUT somewhere else
  * WEBBY Term uses standard keystrokes
 
### Latest Survey Findings from Online Disability Communities by Norbert Rum, Nick Goodrum, and Charlie Beach
