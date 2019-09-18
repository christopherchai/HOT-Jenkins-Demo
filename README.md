**Install Jenkins**
1. Install Jenkins - https://jenkins.io/doc/book/installing/. For this demo, it's easier if you use CentOS - https://pkg.jenkins.io/redhat/
2. Unlock Jenkins - https://jenkins.io/doc/book/installing/ under "Post-installation setup wizard.

**Integrate Jenkins with GitHub**
1. Follow instruction here - https://www.guru99.com/jenkins-github-integration.html
2. Remember to install Git on the same host as Jenkins! Also outlined in the link above.

**Create a Sample Job**
1. Follow the steps outlined here - https://www.guru99.com/create-builds-jenkins-freestyle-project.html
2. For Step 5, use this repository URL - https://github.com/christopherchai/HOT-Jenkins-Demo.git
3. Try to build a successful job. That's about it.

**Getting Jenkins to push deployment events to Dynatrace**
1. Install Dynatrace OneAgent on the Jenkins host. It's okay to restart Jenkins service.
2. Going back to Sample Job in Jenkins, follow the instructions here - https://www.dynatrace.com/support/help/extend-dynatrace/dynatrace-api/environment-api/events/push-deployment-events-from-jenkins/
3. Under Step 10, modify the Request Body as necessary. Make sure tag rules are done correctly, or else you'll get 400 error for your build job. It's easy if you just tag it to the host.
4. Start the build job. You can do it multiple times.
5. In Dynatrace, under Host, you should see Deployment Events happening.

**Getting Dynatrace to push notification to Jenkins and trigger build job**
1. Install Generic Webhook Trigger Plugin in Jenkins.
2. Under Build Triggers, enable Generic Webhook Trigger. Add a token of your choice (I used dynatrace-integration-01).
3. (Optional) Add a cause. I use Dynatrace problem notification.
4. Enable Print post content.
5. In Dynatrace, go to Problem Notification > create Custom Integration.
6. Under webhook URL, input: http://[JENKINS_IP:PORT]/generic-webhook-trigger/invoke?token=[YOUR_TOKEN]
7. Make sure alert profile is correct, then send test notification and save.
8. Manually trigger a problem (i.e. change CPU threshold to 1%)
9. When a problem is flagged out, observe the build job in Jenkins.
10. If there is a new job, go to Console output. You should see something like this:



**Optional: Creating a basic pipeline**
1. Simple warm-up exercise for the upcoming Advanced Jenkins HOT.
2. Following the instructions here: https://www.guru99.com/jenkins-pipeline-tutorial.html
