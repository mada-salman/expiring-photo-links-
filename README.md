# Expiring Photo Links

A secure photo sharing application built on AWS that generates temporary, expiring links for safe and private photo access.

## Overview

Expiring Photo Links is a cloud-based solution for sharing photos securely. It leverages AWS S3 and presigned URLs to provide time-limited access to photos, ensuring privacy and automatic expiration without manual cleanup.

## Features

- **Secure Sharing**: Generate secure, temporary links for photo access
- **Automatic Expiration**: Links automatically expire after a configurable time period
- **AWS S3 Integration**: Leverages AWS S3 for scalable photo storage
- **Presigned URLs**: Uses AWS presigned URLs for secure, temporary access
- **Privacy First**: Photos remain private in S3; access is controlled through temporary tokens
- **Scalable**: Built on AWS infrastructure for reliable, scalable performance

## Tech Stack

- **Frontend**: HTML5, JavaScript
- **Backend**: AWS Lambda, AWS API Gateway (optional)
- **Storage**: AWS S3
- **Authentication**: AWS IAM

## Prerequisites

- AWS Account with access to S3
- Node.js (for local development)
- AWS CLI configured with appropriate credentials

## Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/mada-salman/expiring-photo-links-.git
   cd expiring-photo-links-
   ```

2. **Set up AWS S3**
   - Create an S3 bucket for storing photos
   - Configure bucket policies for presigned URL access
   - Enable CORS if needed for web access

3. **Configure AWS credentials**
   ```bash
   aws configure
   ```

4. **Run locally**
   - Open `index.html` in your browser
   - Or use a local server:
   ```bash
   python -m http.server 8000
   # or
   npx http-server
   ```

## Usage

### Generating Expiring Links

1. Upload a photo to your S3 bucket
2. Use the application to generate a presigned URL with your desired expiration time
3. Share the generated link with recipients
4. The link will automatically expire after the specified duration

### Example

```javascript
// Generate a presigned URL that expires in 1 hour
const expirationTime = 3600; // seconds
const link = generatePresignedUrl(bucketName, photoKey, expirationTime);
```

## Configuration

Configure the following environment variables or settings:

- `AWS_S3_BUCKET`: Your S3 bucket name
- `AWS_REGION`: AWS region (e.g., us-east-1)
- `LINK_EXPIRATION_TIME`: Default expiration time in seconds (default: 3600)

## Security

- Photos remain private in S3 and are not publicly accessible
- Access is controlled through AWS presigned URLs
- Links automatically expire, preventing indefinite access
- Implement additional authentication as needed for your use case

## File Structure

```
expiring-photo-links-/
├── index.html          # Main application interface
├── README.md          # This file
└── .gitignore         # Git ignore rules
```

## Development

### Local Testing

1. Install dependencies (if applicable)
   ```bash
   npm install
   ```

2. Set up local environment variables
   ```bash
   export AWS_S3_BUCKET=your-bucket-name
   export AWS_REGION=us-east-1
   ```

3. Start a local development server
   ```bash
   npm run dev
   # or
   python -m http.server 8000
   ```

## Deployment

For production deployment:

1. **AWS Lambda**: Deploy serverless backend functions
2. **CloudFront**: Use CloudFront for CDN distribution
3. **API Gateway**: Set up API endpoints for photo operations
4. **S3 Static Hosting**: Host frontend on S3 with CloudFront

## Best Practices

- Always use HTTPS for production
- Implement proper AWS IAM roles and policies
- Monitor S3 access with CloudTrail
- Set up CloudWatch alerts for unusual activity
- Regularly review and rotate AWS credentials
- Use environment variables for sensitive configuration

## Troubleshooting

### Presigned URLs Not Working
- Verify AWS credentials are configured correctly
- Check S3 bucket permissions and policies
- Ensure the object exists in S3 before generating a presigned URL

### CORS Issues
- Configure S3 bucket CORS settings
- Verify CORS headers are properly set

### Link Expiration Issues
- Verify the expiration time format is in seconds
- Check server time synchronization

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is open source and available under the MIT License.

## Support

For issues, questions, or suggestions, please open an issue on the GitHub repository.

## Roadmap

- [ ] User authentication
- [ ] Photo upload interface
- [ ] Link management dashboard
- [ ] Analytics and logging
- [ ] Mobile app support
- [ ] Advanced access controls

---

**Built with ❤️ using AWS**
