# Video on Demand on AWS-CHINA

### 前提要求:
* [AWS Command Line Interface](https://aws.amazon.com/cli/)
* Node.js 10.x or later
* Python 3.7 or later

### 1.运行 run-unit tests.sh文件
Run unit tests to make sure added customization passes the tests:
```
cd ./deployment
chmod +x ./run-unit-tests.sh
./run-unit-tests.sh
```

### 2. 创建一个Amazon S3桶
CloudFormation template 被配置为从正在启动该模板的区域中的 Amazon S3 存储桶中提取 Lambda 部署包。在所需区域中创建一个存储桶，（例如，my-bucket）。
```
aws s3 mb s3://my-bucket
```

### 3. 创建部署包
Build the distributable:
```
chmod +x ./build-s3-dist.sh
./build-s3-dist.sh my-bucket video-on-demand-on-aws v5.0.0-custom
```

> **Notes**: The _build-s3-dist_ script expects the bucket name as one of its parameters, and this value should not include the region suffix.

Deploy the distributable to the Amazon S3 bucket in your account:
```
aws s3 cp ./regional-s3-assets/ s3://my-bucket-us-east-1/video-on-demand-on-aws/v5.0.0-custom/ --recursive --acl bucket-owner-full-control
```

### 4. Launch the CloudFormation template.
Use the S3 url contain your video-on-demand-on-aws.template under deployment/dist folder For example: https://vod-mediaconvert-workshop-ray.s3.cn-northwest-1.amazonaws.com.cn/video-on-demand-on-aws/cn-quickstart/video-on-demand-on-aws.template
Specify your parameters and create the stack
Once the stack be executed successfully, record the outputs of stack
## Additional Resources
### Services
- [AWS Elemental MediaConvert](https://aws.amazon.com/mediaconvert/)
- [AWS Elemental MediaPackage](https://aws.amazon.com/mediapackage/)
- [AWS Step Functions](https://aws.amazon.com/mediapackage/)
- [AWS Lambda](https://aws.amazon.com/lambda/)
- [Amazon CloudFront](https://aws.amazon.com/cloudfront/)
- [OTT Workflows](https://www.elemental.com/applications/ott-workflows)
- [QVBR and MediaConvert](https://docs.aws.amazon.com/mediaconvert/latest/ug/cbr-vbr-qvbr.html)

### Other Solutions and Demos
- [Live Streaming On AWS](https://aws.amazon.com/answers/media-entertainment/live-streaming/)
- [Media Analysis Solution](https://aws.amazon.com/answers/media-entertainment/media-analysis-solution/)
- [Live Streaming and Live to VOD Workshop](https://github.com/awslabs/speke-reference-server)
- [Live to VOD with Machine Learning](https://github.com/aws-samples/aws-elemental-instant-video-highlights)
- [Demo SPEKE Reference Server](https://github.com/awslabs/speke-reference-server)

***
