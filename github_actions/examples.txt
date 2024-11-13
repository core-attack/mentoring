-- настройка gha in google cloud

#Чтобы авторизоваться в GHA нужно выполнить следующий гайд https://github.com/google-github-actions/auth#setting-up-workload-identity-federation

#создать пул
gcloud iam workload-identity-pools create "your_company-pool" \
--project="your_company" \
--location="global" \
--display-name="your_company workload identity pool"

#get pool
gcloud iam workload-identity-pools list --location="global"

projects/761694718240/locations/global/workloadIdentityPools/your_company-pool

#create provider
gcloud iam workload-identity-pools providers create-oidc "your_company-provider" \
--project="your_company" \
--location="global" \
--workload-identity-pool="your_company-pool" \
--display-name="your_company provider" \
--attribute-mapping="google.subject=assertion.sub,attribute.actor=assertion.actor,attribute.repository=assertion.repository,attribute.aud=assertion.aud" \
--issuer-uri="https://token.actions.githubusercontent.com"

gcloud iam workload-identity-pools providers create-oidc "refund-keeper-provider" \
--project="refundkeeper" \
--location="global" \
--workload-identity-pool="refund-keeper-pool" \
--display-name="Refund keeper provider" \
--attribute-mapping="google.subject=assertion.sub,attribute.actor=assertion.actor,attribute.repository=assertion.repository,attribute.aud=assertion.aud" \
--attribute-condition="assertion.repository_owner == 'your_company-io'" \
--issuer-uri="https://token.actions.githubusercontent.com"

gcloud iam workload-identity-pools providers update-oidc "your_company-provider" \
--project="your_company" \
--location="global" \
--workload-identity-pool="your_company-pool" \
--display-name="your_company provider" \
--attribute-mapping="google.subject=assertion.sub,attribute.actor=assertion.actor,attribute.repository=assertion.repository,attribute.aud=assertion.aud" \
--issuer-uri="https://token.actions.githubusercontent.com"

gcloud iam workload-identity-pools providers update-oidc "refund-keeper-provider" \
--project="refundkeeper" \
--location="global" \
--workload-identity-pool="refund-keeper-pool" \
--display-name="Refund keeper provider" \
--attribute-mapping="google.subject=assertion.sub,attribute.actor=assertion.actor,attribute.repository=assertion.repository,attribute.aud=assertion.aud" \
--issuer-uri="https://token.actions.githubusercontent.com"

#add repos
gcloud iam service-accounts add-iam-policy-binding "github-actions@your_company.iam.gserviceaccount.com" \
--project="your_company" \
--role="roles/iam.workloadIdentityUser" \
--member="principalSet://iam.googleapis.com/projects/761694712240/locations/global/workloadIdentityPools/your_company-pool/attribute.repository/core-attack/mentoring"

# Updated IAM policy for serviceAccount [github-actions@your_company.iam.gserviceaccount.com].
# bindings:
# - members:
#   - serviceAccount:github-actions@your_company.iam.gserviceaccount.com
#   role: roles/iam.serviceAccountTokenCreator
# - members:
#   - principalSet://iam.googleapis.com/projects/761694712240/locations/global/workloadIdentityPools/your_company-pool/attribute.repository/core-attack/mentoring
#   role: roles/iam.workloadIdentityUser
# etag: BwYXOJN4hOo=
# version: 1

#get provider
gcloud iam workload-identity-pools providers describe "your_company-provider" \
--project="your_company" \
--location="global" \
--workload-identity-pool="your_company-pool" \
--format="value(name)"

projects/761694718240/locations/global/workloadIdentityPools/your_company-pool/providers/your_company-provider
github-actions@your_company.iam.gserviceaccount.com

gcloud iam service-accounts add-iam-policy-binding github-actions@your_company.iam.gserviceaccount.com --project="your_company" --role="roles/iam.serviceAccountTokenCreator" --member="serviceAccount:github-actions@your_company.iam.gserviceaccount.com"

gcloud projects add-iam-policy-binding my-project-123 --role=roles/editor --member=serviceAccount:example@project-id.iam.gserviceaccount.com
