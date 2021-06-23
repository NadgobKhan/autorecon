# Autorecon

### This project revolves around the idea of automating the recon process in a bug bounty assignment.
The main inspiration was the contents of the paper called "Automating Bug Bounty" by Ján Masarik.  
The goal is to create a framework that is able to enumerate subdomains and assets for a certain target, parse and format the results and upload them in GitLab (or other VCS).  
Based on the differences (new domains, new assets), some events will get triggered and notifications(Slack messages, mails) will get sent, thus completing the integration.  
  
  ## End results  
  * achieving continuous monitoring over a certain target
    * this gives the researcher insights of changes through time and helps him/her create a clearer picture of the target
  * be able to effortlessly integrate new tools into the workflow
    * besides subdomain and asset enumeration, these tools could include automatic vulnerability scanners, technology mappers etc

## Technologies used
 * **Kubernetes**
   * used for initial deployment of the below technologies
 * **Sealed Secrets**: https://github.com/bitnami-labs/sealed-secrets
   * used to encrypt secrets in such a way that the manifest could be uploaded to Git securely, without the risk of information leakage, thus achieving full GitOps management
 * **Argo CD**: https://argoproj.github.io/projects/argo-cd/
   * used for managing the workflows, events and other resources in a declarative, GitOps manner  
 * **Argo Events**: https://argoproj.github.io/projects/argo-events/
   * used to register certain event to listen and react to (example: listening for "webhook" events that contain the target which, in turn, trigger the scanning workflows)
 * **Argo Workflows**: https://argoproj.github.io/projects/argo/
   * used orchestrate the order in which the working pods get created (example: the pods that run the subdomain enumeration tools get created before the result parsing pods) 

