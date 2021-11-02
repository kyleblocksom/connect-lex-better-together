**Amazon Connect and Amazon Lex: Better Together**

Deliver Omnichannel Customer Experiences with Interactive Voice Response (IVR) Enabled Contact Centers and Natural Language Processing (NLP) Chatbots – All Backed by Customer Sentiment Analysis

![Shape1](RackMultipart20211102-4-mlg76b_html_a41c42a9d42e0349.gif)

When is the last time you, as a customer, consumed a service or purchased a product? Did you interact with the service or product digitally or in-person? What if you had the flexibility to engage through multiple preferred channels (voice calls, digital chatbots, web-based interaction)? Your modern business is expected to deliver an omnichannel customer experience that unifies customer interactions across multiple channels into one seamless customer journey. Within Banking and Mortgage verticals, an omnichannel customer experience entails users availing all banking operations from a website, mobile application, physical branch location, call center, and other available channels, while context is maintained across all customer associations.

Iterating further on the seamless customer journey concept, you can derive customer sentiment from customer interconnections across your platforms. By identifying and extracting the relevant call and chat logs, website dwell times, and other pertinent source material, you develop a deep understanding of customer sentiment towards your services, products, employees, and more broadly, your brand, allowing you to iteratively improve the overall experience for your customers.

With Amazon Connect and Amazon Lex, you are able to offer your customers the flexible user experience they desire while maintaining a holistic view of their cross-platform engagement. By enabling customers with a self-service capability, you maximize the productivity of your call agents and skills-based work types while also minimizing the operational costs associated with human workforce supply.

# Omnichannel User Interface Overview:

# Once you navigate to the Mortgage Lender/Retail Bank&#39;s AWS Amplify-powered website, you will see the below home screen with your Amazon Lex chatbot embedded within the bottom-right of your screen. The Amazon Lex chatbot then prompts the user for their 4-digit PIN before beginning to fulfill user intents. Let&#39;s get started by building our Amazon Lex chatbot!

![](RackMultipart20211102-4-mlg76b_html_37bf25c96000bb35.png)

**2-Part Omnichannel Deployment Process:**

1. Provision backend services through AWS CloudFormation (AWS Amplify, Amazon DynamoDB, Amazon Kendra, AWS Lambda, and Amazon S3).

1. Import your Amazon Lex chatbot then integrate with Amazon Connect, Twilio SMS, and Slack.

The below architecture diagram illustrates your resultant solution architecture following the above deployment process:

![Shape2](RackMultipart20211102-4-mlg76b_html_5e1c91108f7296d1.gif)

**Deployment Part-1:** Provisioning backend services through AWS CloudFormation

(AWS Amplify, Amazon DynamoDB, Amazon Kendra, and AWS Lambda).

**What are you deploying?**

In Part-1 of your application architecture, you will build an Amazon Lex chatbot that understands customers&#39; speech and text inputs. Your chatbot is embedded within a website created using AWS Amplify which is connected to the source repository that hosts our HTML, JavaScript, and CSS code. Data about available plans and users&#39; chosen plans are persisted in Amazon DynamoDB. AWS Lambda functions are triggered by Amazon Lex to execute business logic and interact with the database layer to query pertinent customer data and fulfill customer requests. Amazon Kendra also allows our chatbot to query against an indexed FAQ document so customers and call center agents can quickly find answers. You can also connect the Amazon Lex chatbot with Twilio SMS and Amazon Connect, which allows users to interact with your chatbot over SMS text messages and call your customer service number and interact with Amazon Lex&#39;s Interactive Voice Response (IVR).

| **Region** | **Region Code** | **Launch** |
| --- | --- | --- |
| US East (N. Virginia) | us-east-1 | omni-lex.yaml |
| --- | --- | --- |

**CloudFormation Launch Instructions:**

1. Select the  **Launch Stack**  link above.
2. Select  **Next**  on the Specify template page.
3. Enter your _\&lt;Stack-name\&gt;_ on the Specify stack details page and select **Next**.
4. On the Configure stack options page, leave all the defaults and click  **Next**.
5. On the Review page, check all the boxes to acknowledge that CloudFormation will create IAM resources.
6. Select  **Create stack**.

Allow CloudFormation to launch your resources in the background; you do not need to wait for it to finish before proceeding to Deployment Part-2.

**Deployment Part-2:** Creating your Amazon Lex bot with Amazon Connect, Twilio SMS, and Slack integration through step-by-step guidance.

**Amazon Lex Concepts:**

- **Inten** t: An intent represents an action that the user wants to perform. You create a bot to support one or more related intents. For example, you might create a bot that orders pizza and drinks. For each intent, you provide the following required information:

  - **Intent name** : A descriptive name for the intent. For example, _OrderPizza_. Intent names must be unique within your account.

  - **Sample utterances** : How a user might convey the intent. For example, a user might say &quot;Can I order a pizza please&quot; or &quot;I want to order a pizza&quot;.

  - **How to fulfill the intent**  – How you want to fulfill the intent after the user provides the necessary information (for example, place order with a local pizza shop). We recommend that you create a Lambda function to fulfill the intent. You can optionally configure the intent so Amazon Lex simply returns the information back to the client application to do the necessary fulfillment.

In addition to custom intents such as ordering a pizza, Amazon Lex also provides built-in intents to quickly set up your bot. For more information, see [Built-in Intents and Slot Types](https://docs.aws.amazon.com/lex/latest/dg/howitworks-builtins.html).

  - **Slot** : An intent can require zero or more slots or parameters. You add slots as part of the intent configuration. At runtime, Amazon Lex prompts the user for specific slot values. The user must provide values for all _required_ slots before Amazon Lex can fulfill the intent. For example, the _OrderPizza_ intent requires slots such as pizza size, crust type, and number of pizzas. In the intent configuration, you add these slots. For each slot, you provide slot type and a prompt for Amazon Lex to send to the client to elicit data from the user. A user can reply with a slot value that includes additional words, such as &quot;large pizza please&quot; or &quot;let&#39;s stick with small.&quot; Amazon Lex can still understand the intended slot value.

  - **Slot type** : Each slot has a type. You can create your custom slot types or use built-in slot types. Each slot type must have a unique name within your account. For example, you might create and use the following slot types for the _OrderPizza_ intent:

    - Size: With enumeration values Small, Medium, and Large.
    - Crust: With enumeration values Thick and Thin.

Amazon Lex also provides built-in slot types. For example, AMAZON.NUMBER is a built-in slot type that you can use for the number of pizzas ordered. For more information, see [Built-in Intents and Slot Types](https://docs.aws.amazon.com/lex/latest/dg/howitworks-builtins.html).

**Amazon Lex Implementation:**

Import Your Amazon Lex Chatbot:

      1. Navigate to the [Amazon Lex Console](https://console.aws.amazon.com/lex/home?region=us-east-1) and select the _Action_ dropdown before selecting _Import._
      2. Select _Browse_ and choose the _omni-lex.zip_ file.
      3. Select the newly created _OmniLex_ under _Bots._
      4. Select _FAQ_ under _Intents_ on the left menu and ensure the _Lex-Kendra-Index_ is selected under _Amazon Kendra query_. Also, ensure your _Response_ section matches the below:

![](RackMultipart20211102-4-mlg76b_html_6bc80a5e4dfa12c1.png)

      1. Select _MakePayment_ under _Intents_ on the left menu:

        1. Under _Lambda initialization and validation_, select _Initialization and validation code hook_ then choose your Lambda function _\&lt;Stack-name\&gt;-OmniLexHandler_ from the dropdown. The version or alias should be set to _Latest._ Select _OK_ when prompted to give Amazon Lex permission to invoke your Lambda Function.

        1. Under _Fulfillment_, select _AWS Lambda function_ then choose your Lambda function _\&lt;Stack-name\&gt;-OmniLexHandler_ from the dropdown with the version or alias set to _Latest._

      1. Select _OpenAccount_ under _Intents_ on the left menu:

        1. Under _Lambda initialization and validation_, select _Initialization and validation code hook_ then choose your Lambda function _\&lt;Stack-name\&gt;-OmniLexHandler_ from the dropdown. The version or alias should be set to _Latest._ Select _OK_ when prompted to give Amazon Lex permission to invoke your Lambda Function.

        1. Under _Fulfillment_, select _AWS Lambda function_ then choose your Lambda function _\&lt;Stack-name\&gt;-OmniLexHandler_ from the dropdown with the version or alias set to _Latest._

      1. Select _ProvideAccountDetails_ under _Intents_ on the left menu:

        1. Under _Lambda initialization and validation_, select _Initialization and validation code hook_ then choose your Lambda function _\&lt;Stack-name\&gt;-OmniLexHandler_ from the dropdown. The version or alias should be set to _Latest._ Select _OK_ when prompted to give Amazon Lex permission to invoke your Lambda Function.

      1. Select _VerifyIdentity_ under _Intents_ on the left menu:

        1. Under _Fulfillment_, select _AWS Lambda function_ then choose your Lambda function _\&lt;Stack-name\&gt;-OmniLexHandler_ from the dropdown with the version or alias set to _Latest._ Select _OK_ when prompted to give Amazon Lex permission to invoke your Lambda Function.

      1. Select _Build_ to assemble your chatbot, then test your chatbot using the dialogue box.

![](RackMultipart20211102-4-mlg76b_html_6deb1739e4529e21.png)

![](RackMultipart20211102-4-mlg76b_html_6335dce1f1932ed8.png)

Configure Twilio SMS Integration with Your Amazon Lex Chatbot:

  1. [Create Twilio SMS Account](https://www.twilio.com/console).

To associate your Amazon Lex chatbot with your Twilio programmable SMS endpoint, we need to activate bot channel association in the Amazon Lex console. When the bot channel association has been activated, Amazon Lex returns a callback URL that we can use for Twilio SMS integration.

  1. Sign in to the [Amazon Lex Console](https://console.aws.amazon.com/lex/).
  2. Select _\&lt;your-bot-name\&gt;._
  3. Navigate to the _Channels_ tab.
  4. In the _Channels_ section, select _Twilio SMS_.
  5. On the _Twilio SMS_ page, provide the following information:

1. Channel name: LexTwilioAssociation
2. Select &quot;aws/lex&quot; from _KMS key_.
3. For _Alias_, select your bot alias.
4. For _Authentication Token_, enter the AUTH TOKEN for your Twilio account.
5. For _Account SID_, enter the ACCOUNT SID for your Twilio account.

  1. Select _Activate_.

![](RackMultipart20211102-4-mlg76b_html_cfbbb4e5ef0db382.png)

The console creates the bot channel association and returns a Callback URL - Record this URL.

  1. On the [Twilio Console](https://www.twilio.com/console), navigate to _Programmable Messaging._
  2. Select _Messaging Services_.
  3. Enter your Amazon Lex generated Callback URL into the _Request URL_ field:

![](RackMultipart20211102-4-mlg76b_html_71be1789b154347a.png)

  1. Enter your Twilio-provided SMS number into the _Sender Pool_:

![](RackMultipart20211102-4-mlg76b_html_25ec8e21e33626e9.png)

  1. Use your mobile phone to test the integration between Twilio SMS and your Amazon Lex chatbot by texting your Twilio-provided SMS number with a sample utterance.

![](RackMultipart20211102-4-mlg76b_html_2695a869d2df7b6e.jpg) ![](RackMultipart20211102-4-mlg76b_html_6025b2efb7dbf3ed.jpg)

Configure Slack Integration with Your Amazon Lex Chatbot:

  1. [Sign Up for Slack and Create Slack Team](https://slack.com/help/articles/212675257-Join-a-Slack-workspace).

To associate your Amazon Lex chatbot with your Slack Application, we need to activate bot channel association in the Amazon Lex console. When the bot channel association has been activated, Amazon Lex returns a callback URL that we can use for Slack Application integration.

  1. Sign in to the [Amazon Lex Console](https://console.aws.amazon.com/lex/).
  2. Select _\&lt;your-bot-name\&gt;._
  3. Navigate to the _Channels_ tab.
  4. In the _Channels_ section, select _Twilio SMS_.
  5. On the _Twilio SMS_ page, provide the following information:

1. Channel name: LexTwilioAssociation
2. Select &quot;aws/lex&quot; from _KMS key_.
3. For _Alias_, select your bot alias.
4. For _Authentication Token_, enter the AUTH TOKEN for your Twilio account.
5. For _Account SID_, enter the ACCOUNT SID for your Twilio account.

  1. Select _Activate_.

![](RackMultipart20211102-4-mlg76b_html_aca4b0a82abe48c8.png)

**Customer Sentiment Analysis User Interface Overview:**

# Once you navigate to the Mortgage Lender/Retail Bank&#39;s customer sentiment analysis dashboard, you will see the below home screen with a sortable list of your Amazon Connect call recordings and Amazon Lex transaction logs. Selecting one of the call recordings or transaction logs leads you to the subsequent screenshot which shows the interaction metadata, language used, average and trending caller and agent sentiment, call or chat duration, and a graph of caller and agent sentiment throughout the interaction. Let&#39;s get started with our simple 3-step AWS CloudFormation deployment process!

![](RackMultipart20211102-4-mlg76b_html_a2a8e7a065761235.png)

![](RackMultipart20211102-4-mlg76b_html_b343c0ad70eb67c4.png)

**3-Part Customer Sentiment Analysis Deployment Process:**

1. Create AWS Systems Manager Parameter Store by deploying AWS CloudFormation template and specifying AWS CloudFormation parameter values.
2. Provision backend services by installing code dependencies, creating AWS Lambda layer, then packaging and deploying AWS CloudFormation template ().
3. Provision frontend customer sentiment analysis user-interface by installing code dependencies then packaging and deploying CloudFormation template ().

The below architecture diagram illustrates your resultant solution following the above deployment:

![](RackMultipart20211102-4-mlg76b_html_14bcb6057df032d3.png)

**Deployment Part-1:** Create AWS Systems Manager Parameter Store by deploying AWS CloudFormation template and specifying AWS CloudFormation parameter values.

**What are you deploying?**

Part-1 of your customer sentiment analysis backend provisions AWS Systems Manager Parameter Store values that will used in subsequent deployment steps to identify variable like your call recording S3 Bucket name and the name of the S3 Bucket that will hold your transcribed call recordings.

| **Region** | **Region Code** | **Launch** |
| --- | --- | --- |
| US East (N. Virginia) | us-east-1 | cfn/ssm.template |
| --- | --- | --- |

**CloudFormation Launch Instructions (expand for details)**

1. Select the  **Launch Stack**  link above.
2. Select  **Next**  on the Specify template page.
3. Enter your _\&lt;Stack-name\&gt;_ on the Specify stack details page and select **Next**.
4. On the Configure stack options page, leave all the defaults and click  **Next**.
5. On the Review page, check all the boxes to acknowledge that CloudFormation will create IAM resources.
6. Select  **Create stack**.

Wait for the _CREATE\_COMPLETE_ status on your CloudFormation stack; you need to wait for it to finish before proceeding to Deployment Part-2.

| **Key** | **Default Value** | **Description** |
| --- | --- | --- |
| BulkUploadBucket | omni-lex-sentiment-bulk-upload |
S3 Bucket into which bulk call recordings and chat transaction logs can be dropped – AWS Step Functions execution required for processing.
 |
| BulkUploadMaxDripRate | 50 | Maximum number of files that the bulk uploader will move to _ **InputBucketName** _per iteration. |
| BulkUploadMaxTranscribeJobs | 250 |
Maximum number of concurrent Amazon Transcribe jobs (executing or queuing) bulk upload will execute.
 |
| ComprehendLanguages |

en | es | fr | de | it | pt |ar | hi | ja | ko | zh | zh-TW
 |
Languages supported by Amazon Comprehend&#39;s standard calls, separated by &quot;|&quot;
 |
| ContentRedactionLanguages | en-US |
Languages supported by Transcribe&#39;s Content Redaction feature, separated by &quot;|&quot;
 |
| ConversationLocation | America/Toronto |
Name of the timezone location for the call source - this [is the](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)[**TZ database name**](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)[from](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)[https://en.wikipedia.or](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)[g](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)[/wiki/List](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)[\_](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)[of](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)[\_](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)[tz](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)[\_](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)[database](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)[\_](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)[time](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)[\_](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)[zones](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)
 |
| EntityRecognizerEndpoint | undefined |
Name of the built custom entity recognizer for Amazon Comprehend (not including language suffix, e.g. -en). If one cannot be found then simple entity string matching is attempted.
 |
| EntityStringMap | simple-entity-list.csv |

Basename of a CSV file containing item/Entity maps forwhen not enough data is present for Comprehend Custom Entities (not including language suffix, e.g. -en).
 |
| EntityThreshold | 0.5 |
Confidence threshold where custom entity detection result is accepted.
 |
| InputBucketAudioPlayback | mp3 |
Folder that holds browser audio playback.
 |
| InputBucketFailedTranscriptions | failedAudio |
Folder that holds audio failed transcription files.
 |
| InputBucketName | omni-lex-sentiment-source-audio |
S3 Bucket into which audio files are delivered.
 |
| InputBucketRawAudio | originalAudio |
Folder that holds the raw call audio.
 |
| MaxSpeakers | 2 |
Maximum number of speakers that are expected on a call.
 |
| MinSentimentNegative | 0.4 |
Minimum sentiment level required to declare a phrase as having negative sentiment.
 |
| MinSentimentPositive | 0.4 |
Minimum sentiment level required to declare a phrase as having positive sentiment.
 |
| OutputBucketName | omni-lex-sentiment-transcribe-output |
S3 Bucket into which Amazon Transcribe output files are delivered.
 |
| OutputBucketParsedResults | parsedFiles |
Folder within the output S3 Bucket into which parsed results are written.
 |
| SpeakerNames | Agent | Caller |
Default tags used for speaker names, separated by a &quot;|&quot;
 |
| SpeakerSeparationType | Speaker |
 ![Shape3](RackMultipart20211102-4-mlg76b_html_f82412c3af3a0c37.gif)Separation mode for speakers, (speaker, channel, or auto).
 |
| StepFunctionName | PostCallAnalyticsWorkflow |
Name of AWS Step Functions sentiment analysis workflow.
 |
| SupportFilesBucketName | omni-lex-sentiment-custom-source-files |
S3 Bucket that hold supporting files, such as the file-based entity recognition mapping files.
 |
| TranscribeAlternateLanguage | en-US |
Allows files delivered from a non-standard S3 Bucket to be based upon this language.
 |
| ![Shape4](RackMultipart20211102-4-mlg76b_html_dcea502fcb8261bb.gif)TranscribeLanguages | en-US |
Language to be used for transcription - multiple entries separated by &quot;|&quot; will trigger Language Detection using those languages; if that fails for any reason then the first language in this list is used for transcription.
 |
| VocabularyName | undefined |
Name of the custom vocabulary to use for Amazon Transcribe (excluding language suffix).
 |

**Deployment Part-2:** Provision backend services by installing code dependencies, creating AWS Lambda layer, then packaging and deploying AWS CloudFormation template.

\*\*link to download to source code folder\*\*

1. Install code dependencies:

cd src/trigger

npm i

cd src/pca
 pip install -t . -r requirements.txt

1. Upload _ffmpeg.zip_ file to the S3 bucket defined in the configuration parameter _SupportFilesBucketName_ as specified in Part-1 of your customer sentiment analysis deployment.
2. Using the AWS CLI, enter the following to package and deploy your AWS CloudFormation template, replacing the below values:

| **Name** | **Value** |
| --- | --- |
| \&lt;bucket\&gt; | Name of the S3 bucket that will hold packaged AWS Lambda code during deployment |
| \&lt;stack\&gt; | Name of the CloudFormation stack |

cd cfn

aws cloudformation package --template-file main.template \

--output-template-file packaged.template \

--s3-bucket \&lt;bucket\&gt;

aws cloudformation deploy --template-file packaged.template \

--stack-name \&lt;stack\&gt; \

--capabilities CAPABILITY\_NAMED\_IAM CAPABILITY\_AUTO\_EXPAND

**Deployment Part-3:** Provision frontend customer sentiment analysis user-interface by installing code dependencies then packaging and deploying CloudFormation template.

1. Install code dependencies:

cd src/lambda

npm install

1. Using the AWS CLI, enter the following to package and deploy your AWS CloudFormation template, replacing the below values:

| **Name** | **Value** |
| --- | --- |
| \&lt;YOUR\_BUCKET\&gt; | Name of the S3 bucket in your account to store packaged AWS Lambda functions |
| \&lt;STACK\_NAME\&gt; | Name of the CloudFormation stack |

cd cfn

aws cloudformation package \
 --template-file main.template \

--output-template-file packaged.template \

--s3-bucket \&lt;YOUR\_BUCKET\&gt;

aws cloudformation deploy \
--template-file packaged.template \
--stack-name \&lt;STACK\_NAME\&gt; \
--capabilities CAPABILITY\_IAM CAPABILITY\_AUTO\_EXPAND

1. Add users to Cognito by navigating to the [Amazon Cognito console](https://console.aws.amazon.com/cognito/home?region=us-east-1) and locating the User Pool that was deployed by AWS CloudFormation in the previous step. Administrators will use these logins to access your customer sentiment analysis dashboard.

  1. Go to _Users and Groups._
  2. Add users as required.

Your implementation is complete! You successfully deployed and configured the below architecture:

![](RackMultipart20211102-4-mlg76b_html_851742ee98d6d393.png)
