pipeline {
  agent any
  stages {
    stage('Create Instance template with MIG and LB') {
      steps {
        sh 'gcloud compute instance-templates create nginx-template --project=my-project-279-436907 --region us-central1 --machine-type=e2-medium --metadata-from-file startup-script=./startup.sh --service-account=jenkis-github@my-project-279-436907.iam.gserviceaccount.com'
        sh 'gcloud compute target-pools create nginx-pool --region us-central1'
        sh 'gcloud compute instance-groups managed create nginx-group --base-instance-name nginx --size 2 --template nginx-template --target-pool nginx-pool --region=us-central1'
        sh 'gcloud compute firewall-rules create www-firewall --allow tcp:80'
        sh 'gcloud compute forwarding-rules create nginx-lb --region us-central1 --ports=80 --target-pool nginx-pool'
      }
    }
  }
}
