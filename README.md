# Photo Sharer - Expiring Photo Links

A lightweight, serverless photo sharing application that generates secure, time-limited download links. Upload a photo and instantly get an expiring link to share safely.

## Overview

Photo Sharer is a minimalist, privacy-first photo sharing application built on AWS serverless infrastructure. It allows users to:
- Upload photos directly to Amazon S3
- Generate time-limited presigned URLs for safe sharing
- Control link expiration time (in seconds)
- Share photos without storing them permanently accessible

Perfect for sharing sensitive photos, temporary file transfers, or confidential images that should self-destruct after a set time.

## Features

✨ **Key Features:**
- **One-Click Upload**: Select and upload photos with a single click
- **Customizable Link Expiration**: Set expiration time from 60 seconds to any duration
- **Presigned URLs**: Generate AWS S3 presigned URLs for secure, time-limited access
- **No Database Required**: Serverless architecture using AWS Lambda and S3
- **Beautiful UI**: Modern, responsive interface with Tailwind CSS
- **Real-time Status**: Live feedback during upload and link generation
- **Privacy-Focused**: Photos are stored privately in S3; access controlled via presigned URLs

## Tech Stack

- **Frontend**: HTML5, JavaScript, Tailwind CSS
- **Backend**: AWS Lambda (serverless function)
- **Storage**: Amazon S3
- **Architecture**: Serverless (no servers to manage)

## How It Works

1. **Upload Phase**: 
   - User selects a photo file
   - Frontend requests a presigned upload URL from Lambda
   - File is uploaded directly to S3 using the presigned URL

2. **Link Generation Phase**:
   - User sets desired link expiration time (default: 3600 seconds / 1 hour)
   - Lambda generates a presigned download URL
   - URL is displayed and ready to share

3. **Expiration**:
   - AWS automatically invalidates the presigned URL after the specified time
   - Link becomes inaccessible without regeneration

## Getting Started

### Prerequisites

- AWS Account with Lambda and S3 access
- A web browser
- An AWS Lambda function URL (see setup below)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/mada-salman/expiring-photo-links-.git
   cd expiring-photo-links-
   ```

2. **Deploy Lambda Backend** (Required)
   - You need a Lambda function that handles:
     - Generating presigned upload URLs
     - Generating presigned download URLs
   - Create a Lambda function and get its Function URL

3. **Configure Frontend**
   - Open `index.html` in a text editor
   - Find line 232: `const combinedLambdaUrl = "..."`
   - Replace with your Lambda Function URL

4. **Host the Frontend**
   - Option A: Host on AWS S3 with CloudFront
   - Option B: Deploy to any static hosting (GitHub Pages, Netlify, Vercel)
   - Option C: Open `index.html` locally in your browser

### Quick Setup (Local Testing)

```bash
# Start a local web server
python -m http.server 8000
# or
npx http-server

# Visit http://localhost:8000
```

## Usage

### For End Users

1. **Upload a Photo**
   - Click "Click to select photo" or drag and drop
   - Click "Upload Photo"
   - Wait for success message

2. **Generate Expiring Link**
   - Set expiration time in seconds (default: 3600 = 1 hour)
   - Click "Get Link"
   - Share the generated link
   - Link automatically expires after the set time

### Example Expiration Times
- 300 seconds = 5 minutes
- 1800 seconds = 30 minutes
- 3600 seconds = 1 hour (default)
- 86400 seconds = 1 day

## Lambda Backend Requirements

Your Lambda function should accept POST requests with:

```json
{
  "key": "filename.jpg",
  "type": "upload",      // or "download"
  "expires": 300
}
```

And return:

```json
{
  "url": "https://s3.amazonaws.com/bucket/file?X-Amz-Signature=..."
}
```

## Configuration

The frontend is configured via a single variable in `index.html`:

```javascript
const combinedLambdaUrl = "https://your-lambda-function-url.lambda-url.region.on.aws/";
```

This URL should point to your deployed AWS Lambda function.

## File Structure

```
expiring-photo-links-/
├── index.html         # Frontend application (all-in-one file)
├── README.md          # This file
└── .gitignore
```

## Security Considerations

🔒 **Security Features:**
- **Private Storage**: Photos stored privately in S3 bucket
- **Presigned URLs**: Time-limited access tokens instead of permanent links
- **No Permissions Needed**: Users don't need AWS credentials to download
- **Automatic Expiration**: Links become inaccessible after expiration
- **HTTPS Only**: Use HTTPS for all production deployments

**Best Practices:**
- Use CORS properly configured on Lambda/API Gateway
- Ensure S3 bucket is NOT public
- Monitor CloudTrail for unauthorized access attempts
- Use CloudWatch for logging and alerts
- Rotate AWS credentials regularly
- Enable S3 encryption

## Deployment Options

### Option 1: AWS S3 + CloudFront (Recommended)
```bash
# Upload index.html to S3
# Create CloudFront distribution
# Use CloudFront URL for access
```

### Option 2: AWS Amplify
```bash
# Connect GitHub repo to Amplify
# Auto-deploys on push
# Built-in HTTPS and CDN
```

### Option 3: Other Hosting
- GitHub Pages (static hosting)
- Netlify (static hosting)
- Vercel (static hosting)
- Your own web server

## Troubleshooting

### "Error: Failed to get upload URL"
- Check Lambda function URL is correct in `index.html`
- Verify Lambda has S3 permissions (PutObject, GetObject)
- Check CORS configuration on Lambda

### Upload Succeeds But Link Won't Work
- Verify Lambda has GetObject permission on S3
- Check S3 bucket name in Lambda function
- Ensure S3 bucket is not public but Lambda can access it

### Link Expires Immediately
- Check Lambda time synchronization (should match AWS server time)
- Verify `expires` parameter is in seconds, not milliseconds

### Photos Not Appearing in S3
- Verify S3 bucket name in Lambda
- Check IAM permissions for Lambda role
- Enable S3 access logging for debugging

## Browser Compatibility

- Chrome/Edge: ✅ Full support
- Firefox: ✅ Full support
- Safari: ✅ Full support
- IE11: ❌ Not supported

## Performance

- **Upload**: Limited by file size and network speed
- **Link Generation**: ~100-200ms (Lambda cold start may add 1-3 seconds)
- **CDN**: Use CloudFront for global distribution

## Development

### Customization
- Modify CSS in the `<style>` block for branding
- Change color scheme (currently indigo/teal)
- Adjust default expiration time (line 221)

### Adding Features
- Add photo preview before upload
- Add multiple file upload support
- Add photo gallery/history
- Add authentication/user accounts

## Limitations

- Single file upload at a time
- No built-in photo gallery/history
- No user authentication
- Frontend only (backend needed)

## Contributing

Contributions welcome! Please submit issues and pull requests.

## License

This project is open source and available under the MIT License.

## Support

For issues or questions:
1. Check the troubleshooting section
2. Open an issue on GitHub
3. Review AWS Lambda and S3 documentation

## Related Resources

- [AWS Lambda Documentation](https://docs.aws.amazon.com/lambda/)
- [Amazon S3 Documentation](https://docs.aws.amazon.com/s3/)
- [AWS Presigned URLs](https://docs.aws.amazon.com/AmazonS3/latest/userguide/PresignedUrlUploadObject.html)
- [Tailwind CSS](https://tailwindcss.com/)

---

**Built with AWS Serverless Architecture**
