# sup-hcls-generate-clinical-notes-with-ai

These notebooks demonstrate how to use AWS HealthScribe APIs and how to integrate HealthScribe output with Amazon Comprehend Medical and Amazon Bedrock.

## Prerequisites
- Verify that model access to Anthropic's Claude v2 is granted to the account being used, see documentation here: [Amazon Bedrock Model Access](https://docs.aws.amazon.com/bedrock/latest/userguide/model-access.html)

## Setup Instructions
1. These notebooks were designed to run with Amazon SageMaker Studio. To use Studio, you will need to setup a SageMaker Domain. For instructions on how to onboard to a Sagemaker domain, refer to this [link](https://docs.aws.amazon.com/sagemaker/latest/dg/gs-studio-onboard.html).

2. Check for an **AmazonTranscribeServiceRole** in your [IAM console](https://us-east-1.console.aws.amazon.com/iam/home?region=us-east-1#/roles). If you don't have one, you can create it by starting a transcription job on the [HealthScribe console](https://us-east-1.console.aws.amazon.com/transcribe/home?region=us-east-1#createJobHealthScribe) or manually creating the role with necessaryt permissions on the [IAM console](https://us-east-1.console.aws.amazon.com/iam/home?region=us-east-1#/roles/create). Have in mind this role will need access to the S3 buckets used for input and output.

3. Update your SageMaker execution role (created when you initially setup the domain) to assume the HealthScribe role with a policy similar to the one below:

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "iam:GetRole",
                "iam:PassRole"
            ],
            "Resource": [
                "[HEALTHSCRIBE_IAM_ROLE]]"
            ]
        }
    ]
}
```

## Usage Instructions
1. Open SageMaker Studio and import files [HealthScribe.ipynb](HealthScribe.ipynb) and [HealthScribe_Bedrock.ipynb](HealthScribe_Bedrock.ipynb) from this project. The notebooks have to be executed in order (first HeatlhScribe and second HealthScribe_Bedrock) given the second file uses one of the outputs from the first file.
2. Run all cells in the Jupyter Notebooks provided. Each notebook will have a Setup section in the beggining with additional instalation instructions.