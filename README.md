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
