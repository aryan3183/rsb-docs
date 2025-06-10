# Rocket Social Boost

A comprehensive social media automation and growth platform that manages multiple social media platforms through a Discord bot interface.

## Table of Contents
- [Overview](#overview)
- [Features](#features)
- [Installation](#installation)
  - [Prerequisites](#prerequisites)
  - [Requirements](#requirements)
- [Configuration](#configuration)
  - [Core Configuration](#core-configuration)
  - [Webhook Configuration](#webhook-configuration)
  - [Panel Configuration](#panel-configuration)
- [Platform-Specific Documentation](#platform-specific-documentation)
  - [Instagram](#instagram)
    - [Commands](#commands)
    - [Package Types](#package-types)
    - [Post Automation System](#post-automation-system)
    - [Story Automation System](#story-automation-system)
    - [Engagement Distribution](#engagement-distribution)
    - [Time-based Engagement](#time-based-engagement)
  - [LinkedIn](#linkedin)
    - [Commands](#linkedin-commands)
    - [Package Types](#linkedin-package-types)
    - [Post Automation System](#linkedin-post-automation-system)
    - [Automation Workflow](#linkedin-automation-workflow)
    - [API Integration](#linkedin-api-integration)
    - [Error Handling and Monitoring](#linkedin-error-handling-and-monitoring)
    - [Best Practices](#linkedin-best-practices)
  - [TikTok](#tiktok)
    - [Commands](#tiktok-commands)
    - [Package Types](#tiktok-package-types)
    - [Post Automation System](#tiktok-post-automation-system)
    - [Automation Workflow](#tiktok-automation-workflow)
    - [Performance Monitoring](#tiktok-performance-monitoring)
    - [Best Practices](#tiktok-best-practices)
  - [Twitter](#twitter)
    - [Overview](#twitter-overview)
    - [Features](#twitter-features)
    - [Post Automation](#twitter-post-automation)
    - [Engagement Distribution](#twitter-engagement-distribution)
    - [Safety Features](#twitter-safety-features)
    - [Package Types](#twitter-package-types)
    - [Engagement Heatmap](#twitter-engagement-heatmap)
    - [Commands](#twitter-commands)
    - [Configuration](#twitter-configuration)
    - [Best Practices](#twitter-best-practices)
  - [YouTube](#youtube)
  - [Google Business](#google-business)
- [Task Scheduling System](#task-scheduling-system)
  - [New Scheduler](#new-scheduler-newcheckerpy)
  - [Legacy Scheduler](#legacy-scheduler-task_checkerpy)
- [API Integrations](#api-integrations)
  - [Social Media APIs](#social-media-apis)
  - [Service APIs](#service-apis)
  - [SMM Panel Integration](#smm-panel-integration)
- [Commands](#commands)
  - [General Commands](#general-commands)
  - [Moderation Commands](#moderation-commands)
  - [SMM Panel Commands](#smm-panel-commands)
- [Security Notes](#security-notes)
- [Error Handling](#error-handling)
- [Contributing](#contributing)
- [License](#license)

## Overview

Rocket Social Boost is a powerful social media automation platform that helps manage and grow social media presence across multiple platforms. It uses a Discord bot interface for control and monitoring, with support for:

- Instagram (Posts & Stories)
- Twitter
- LinkedIn
- TikTok
- YouTube
- Google Business
- Facebook

## Features

- Multi-platform social media management
- Automated post engagement
- Story automation
- Comment generation using AI
- Engagement analytics and tracking
- Subscription management via Chargebee
- Customizable engagement profiles
- Real-time monitoring and notifications
- Proxy support for API calls

## Installation

### Prerequisites
```bash
# Install dependencies
pip install -r requirements.txt
```

### Requirements
```
aiohttp
bson
colorama
dateutil
discord
openai
pymongo
requests
ipython
```

## Configuration

The system uses a `config.json` file for all configuration settings:

### Core Configuration
```json
{
    "token" : "DISCORD_BOT_TOKEN",
    "prefix": ".",
    "gemini_api_key" : "GEMINI_API_KEY",
    "rapidapi" : "RAPID_API_KEY",
    "chatgpt" : "OPENAI_API_KEY",
    "api_key" : "API_KEY_FOR_PANEL",
    "chargebee" : {
        "api_key" : "Chargebee API KEY",
        "site_name" : "Name of site for chargebee"
    },
    "firstpromoter" : "First promoter API KEY",
    "proxy" : "user:pass@ip:port",
    "mongodb" : "mongodb URL",
    "webhooks" : {
        "orderwebhook" : "WEBHOOK_URL_HERE",
        "youtube" : "WEBHOOK_URL_HERE",
        "spotify" : "WEBHOOK_URL_HERE",
        "instagram" : "WEBHOOK_URL_HERE",
        "tiktok" : "WEBHOOK_URL_HERE",
        "twitter" : "WEBHOOK_URL_HERE",
        "linkedin" : "WEBHOOK_URL_HERE",
        "facebook" : "WEBHOOK_URL_HERE",
        "google" : "WEBHOOK_URL_HERE",
        "subscription_cancelled" : "WEBHOOK_URL_HERE",
        "subscription_renewed" : "WEBHOOK_URL_HERE",
        "subwebhook" : "WEBHOOK_URL_HERE",
        "subscription_error" : "WEBHOOK_URL_HERE",
        "post_checker" : "WEBHOOK_URL_HERE"
    },
    "panels" : [
        {
            "url" : "https://PANEL.com/api/v2",
            "api_key" : "API_KEY_HERE",
            "name" : "Panel Name"
        }
    ],
    "instagram_channel" : "CHANNEL_ID_HERE",
    "followerchecker" : "CHANNEL_ID_HERE",
    "postchecker" : "CHANNEL_ID_HERE"
}
```

### Webhook Configuration
The system uses multiple Discord webhooks for different types of notifications:
- Order notifications
- Platform-specific notifications (YouTube, Spotify, Instagram, etc.)
- Subscription status updates
- Error reporting

### Panel Configuration
The system integrates with multiple SMM panels for service delivery. Each panel configuration includes:
```json
{
    "url": "PANEL_API_URL",
    "api_key": "PANEL_API_KEY",
    "name": "PANEL_NAME"
}
```

## Platform-Specific Documentation

### Instagram
#### Overview
Instagram automation in Rocket Social Boost provides comprehensive management of Instagram accounts, including post automation, story automation, and engagement management. The system supports both regular engagement growth and viral growth packages.

#### Commands
```bash
# User Management Commands
/instagram_user <username>         
    # Get detailed information about an Instagram user
    Arguments:
    - username: Instagram username to look up

/instagram_lookup <username>       
    # Look up and verify Instagram user details
    Arguments:
    - username: Instagram username to verify

/instagram_posts <username>        
    # Display recent posts from a user
    Arguments:
    - username: Instagram username to get posts from

/instagram_adduser                 
    # Add a new user to automation system
    Arguments:
    - username: Instagram username
    - package: Choice[str] - Package type:
        - "Growth Package Monthly/Yearly"
        - "Gold Package Monthly/Yearly"
        - "Diamond Package Monthly/Yearly"
        - "Platinum Package Monthly/Yearly"
        - "VIP Package Monthly/Yearly"
        - "Elite Package Monthly/Yearly"
        - "Small/Medium/Big/Super Viral Monthly"
        - ...Others (grabbed from database)
    - country: Choice[str] - Target country:
        - "USA"
        - "Portuguese"
    - timezone: Choice[str] - User's timezone:
        - "America/Los_Angeles"
        - "America/New_York"
        - "Europe/London"
        - ...Others (must match timezone format)
    - email: Optional[str] - User's email
    - phone_number: Optional[str] - User's phone number

# Automation Control Commands
/pause <username>                  
    # Pause automation for a user
    Arguments:
    - username: Instagram username to pause

/resume <username>                 
    # Resume automation for a user
    Arguments:
    - username: Instagram username to resume

/renew <username>                  
    # Renew user's subscription
    Arguments:
    - username: Instagram username to renew

# Demo Commands
/slowdemoinsta                     
    # Run slow engagement demo
    Arguments:
    - postlink: str - Instagram post URL
    - package: str - Package name to simulate
    - multiplier: float = 1.0 - Engagement multiplier
    - custom_prompt: str = "" - Custom AI prompt to enchance comments for user.

/fastdemoinsta                     
    # Run fast engagement demo
    Arguments:
    - postlink: str - Instagram post URL
    - package: str - Package name to simulate
    - multiplier: float = 1.0 - Engagement multiplier
    - custom_prompt: str = "" - Custom AI prompt to enchance comments for user.

```

#### Post Automation System
The post automation system (`post_automation.py`) provides:

1. **Real-time Post Monitoring**
   - Monitors new posts from subscribed users
   - Triggers automated engagement based on package type
   - Supports both image and video posts

2. **Engagement Features**
   ```python
   # Available Engagement Types
   - Likes
   - Comments (AI-generated)
   - Views (for videos)
   - Saves
   - Shares
   ```

3. **AI-Powered Comment Generation**
   - Uses OpenAI/Gemini for context-aware comments
   - Supports multiple languages
   - Country-specific comment styles
   - Custom prompting for different engagement types

4. **Engagement Distribution**
   ```python
   # Example Distribution Profile
   Profile 1: [50, 30, 20, 0]  # Steady Growth
   Profile 2: [70, 20, 10, 0]  # Fast Rise
   Profile 3: [50, 20, 30, 0]  # Delayed Spike
   Profile 4: [60, 20, 20, 0]  # Long-Tail Growth
   ```

5. **Time-based Engagement**
   - 24-hour Engagement Heatmap Distribution (3-day cycle)
     ```python
     # Hourly engagement distribution (percentage of total daily engagement)
     # Format: [hour 0-23] - Each row represents a day of the week
     Monday:    [0, 0, 0, 0, 0, 0, 0, 0.03, 0.04, 0.06, 0.1, 0.12, 0.12, 0.1, 0.09, 0.09, 0.06, 0.04, 0.03, 0.02, 0.01, 0, 0, 0]
     Tuesday:   [0, 0, 0, 0, 0, 0, 0, 0.02, 0.04, 0.06, 0.1, 0.12, 0.13, 0.12, 0.1, 0.09, 0.08, 0.06, 0.04, 0.03, 0.02, 0, 0, 0]
     Wednesday: [0, 0, 0, 0, 0, 0, 0, 0.03, 0.05, 0.07, 0.1, 0.12, 0.12, 0.1, 0.09, 0.08, 0.07, 0.05, 0.03, 0.02, 0.01, 0, 0, 0]
     Thursday:  [0, 0, 0, 0, 0, 0.01, 0.03, 0.05, 0.07, 0.1, 0.12, 0.14, 0.14, 0.13, 0.1, 0.09, 0.08, 0.07, 0.05, 0.03, 0.02, 0, 0, 0]
     Friday:    [0, 0, 0, 0, 0.01, 0.02, 0.05, 0.07, 0.1, 0.12, 0.14, 0.15, 0.13, 0.11, 0.1, 0.09, 0.08, 0.06, 0.04, 0.03, 0.02, 0, 0, 0]
     Saturday:  [0, 0, 0, 0.01, 0.03, 0.05, 0.07, 0.1, 0.12, 0.14, 0.14, 0.13, 0.12, 0.1, 0.09, 0.08, 0.07, 0.05, 0.03, 0.02, 0.01, 0, 0, 0]
     Sunday:    [0, 0, 0, 0.01, 0.03, 0.05, 0.07, 0.1, 0.12, 0.14, 0.14, 0.13, 0.12, 0.1, 0.08, 0.07, 0.06, 0.05, 0.03, 0.02, 0.01, 0, 0, 0]
     ```

     **How the Heatmap Works:**
     - Each number represents the percentage of total daily engagement for that hour
     - Numbers add up to 1 (100%) for each day
     - Peak hours (11AM-2PM) receive 12-15% of daily engagement
     - Early morning (0-6AM) receives minimal engagement
     - Evening taper (6PM-11PM) shows gradual decrease
     
     **Key Engagement Periods:**
     - Dead Hours (12AM-6AM): 0-1% per hour
     - Rising Period (7AM-10AM): 2-10% per hour
     - Peak Hours (11AM-2PM): 12-15% per hour
     - Sustained Period (2PM-5PM): 8-11% per hour
     - Decline Period (6PM-11PM): 1-7% per hour

     **Day-Specific Patterns:**
     - Weekdays (Mon-Thu): Later start, concentrated mid-day
     - Fridays: Earlier start, higher peak engagement
     - Weekends: Earlier start, more distributed engagement

     **Usage in Automation:**
     - System uses this distribution to schedule engagement actions
     - Adjusts for user's timezone
     - Maintains natural engagement patterns
     - Prevents detection of automated activity

#### Story Automation System
The story automation system (`story_automation.py`) handles:

1. **Story Monitoring**
   - Real-time story detection
   - Automated view count management
   - Engagement timing optimization

2. **View Distribution**
   - Gradual view increase
   - Natural viewing patterns
   - Anti-detection measures

#### Automation Workflow
1. **Post Detection**
   ```mermaid
   graph TD
   A[Monitor User] --> B{New Post?}
   B -->|Yes| C[Analyze Content]
   B -->|No| A
   C --> D[Generate Engagement Plan]
   D --> E[Execute Engagement]
   E --> F[Monitor Results]
   F --> A
   ```

2. **Engagement Distribution**
   - Initial burst (first hour)
   - Steady growth (24 hours)
   - Long-tail engagement (3-7 days)

3. **Safety Features**
   - Rate limiting
   - Anti-spam measures
   - Natural engagement patterns
   - IP rotation through proxies

#### Configuration
```json
{
    "instagram_channel": "CHANNEL_ID",
    "followerchecker": "CHECKER_CHANNEL_ID",
    "postchecker": "POST_CHECKER_CHANNEL_ID"
}
```

#### Error Handling
- Automated retry system for failed engagements
- Discord webhook notifications for:
  - Failed orders
  - Successful engagements
  - System warnings
  - Rate limit notifications

#### Monitoring and Analytics
- Real-time follower growth tracking
- Engagement rate monitoring
- Post performance analytics
- Package effectiveness tracking

### LinkedIn
#### Overview
LinkedIn automation in Rocket Social Boost provides professional engagement automation focused on business growth and professional networking. The system is designed to maintain LinkedIn's professional nature while providing meaningful engagement.

#### Commands
```bash
# User Management
/linkedin_lookup <profile_link>     # Look up and verify LinkedIn profile details
/linkedin_adduser                   # Add a new user to automation system with parameters:
    - profile_link: LinkedIn profile URL
    - package: Growth package selection
    - email: Optional user email
    - phone_number: Optional phone number
```

#### Package Types
```python
# Available Packages
1. LinkedIn Growth Package Monthly
   - Professional engagement optimization
   - Network growth management
   - Content engagement automation
   - Business profile optimization
```

#### Post Automation System
The post automation system (`post_automation.py`) provides:

1. **Real-time Post Monitoring**
   - Continuous profile monitoring
   - New post detection
   - Content type classification
   - Engagement opportunity identification

2. **Engagement Features**
   ```python
   # Available Engagement Types
   - Likes (Professional timing)
   - Comments (AI-generated business content)
   - Views (Profile and post)
   - Reposts (Strategic sharing)
   ```

3. **AI-Powered Professional Comment Generation**
   - Industry-specific terminology
   - Business context awareness
   - Professional tone maintenance
   - Multi-language support

4. **Engagement Distribution**
   ```python
   # Distribution Patterns
   - Business hours focus
   - Geographic time zone adaptation
   - Industry-specific timing
   - Professional network consideration
   ```

5. **Content Type Support**
   - Article posts
   - Image content
   - Video content
   - Document shares
   - Text-only updates

#### Safety and Monitoring
1. **Network Protection**
   - Connection limit monitoring
   - Engagement rate control
   - Professional reputation management
   - Anti-spam measures

2. **Analytics**
   - Network growth tracking
   - Engagement success rates
   - Content performance metrics
   - Professional impact scoring

#### Automation Workflow
1. **Post Detection**
   ```mermaid
   graph TD
   A[Monitor User] --> B{New Post?}
   B -->|Yes| C[Analyze Content]
   C --> D[Generate Engagement Plan]
   D --> E[Execute Strategy]
   E --> F[Monitor Performance]
   F --> A
   B -->|No| A
   ```

2. **Engagement Strategy**
   - Initial boost period
   - Trending phase optimization
   - Sustained engagement
   - Viral potential maximization

3. **Safety Features**
   - Rate limiting
   - Anti-ban measures
   - Content safety checks
   - Platform compliance

#### API Integration
The system integrates with LinkedIn API for:
- Post automation
- Engagement tracking
- Profile monitoring

#### Error Handling and Monitoring
1. **Network Protection**
   - Connection limit monitoring
   - Engagement rate control
   - Professional reputation management
   - Anti-spam measures

2. **Analytics**
   - Network growth tracking
   - Engagement success rates
   - Content performance metrics
   - Professional impact scoring

#### Best Practices
1. **Content Optimization**
   - Trend alignment
   - Hashtag optimization
   - Post timing
   - Content categorization

2. **Growth Strategy**
   - Viral potential maximization
   - Engagement rate optimization
   - Follower retention
   - Content consistency

### TikTok
#### Overview
TikTok automation in Rocket Social Boost provides comprehensive video content engagement management, focusing on viral growth and authentic engagement patterns. The system supports both regular engagement and trending content optimization.

#### Commands
```bash
# User Management
/tiktok_lookup <username>          # Look up and verify TikTok user details
/tiktok_adduser                    # Add new user to automation system with parameters:
    - username: TikTok username
    - package: Package selection
    - email: Optional user email
    - phone_number: Optional phone number

# Demo Commands
/tiktokdemo <postlink>             # Run engagement demo on specific post
```

#### Package Types
```python
# Available Packages
1. TikTok Package Monthly
   - Video view optimization
   - Engagement growth
   - Trending content boost
   - Follower acquisition
```

#### Post Automation System
The post automation system (`post_automation.py`) provides:

1. **Video Content Monitoring**
   - Real-time post detection
   - Video content analysis
   - Trend alignment checking
   - Engagement opportunity identification

2. **Engagement Features**
   ```python
   # Available Engagement Types
   - Views (Primary metric)
   - Likes (Engagement indicator)
   - Comments (AI-generated relevant content)
   - Shares (Viral potential)
   - Saves (Content value metric)
   ```

3. **AI-Powered Comment Generation**
   ```python
   # Comment Generation Features
   - Video content analysis
   - Trend-aware responses
   - Hashtag integration
   - Multi-language support
   - Age-appropriate content
   ```

4. **Custom Batch Processing**
   ```python
   # Engagement Distribution
   - Initial viral push
   - Sustained engagement
   - Trending optimization
   - Geographic distribution
   ```

5. **Media Processing**
   - Thumbnail analysis
   - Video transcript generation
   - Content categorization
   - Trend alignment

#### Automation Workflow
1. **Content Detection**
   ```mermaid
   graph TD
   A[Monitor Account] --> B{New Video?}
   B -->|Yes| C[Analyze Content]
   C --> D[Generate Engagement Plan]
   D --> E[Execute Strategy]
   E --> F[Monitor Performance]
   F --> A
   B -->|No| A
   ```

2. **Engagement Strategy**
   - Initial boost period
   - Trending phase optimization
   - Sustained engagement
   - Viral potential maximization

3. **Safety Features**
   - Rate limiting
   - Anti-ban measures
   - Content safety checks
   - Platform compliance

#### Performance Monitoring
1. **Analytics Tracking**
   - View count progression
   - Engagement ratios
   - Trending potential
   - Follower growth correlation

2. **Safety Metrics**
   - Account health monitoring
   - Engagement rate safety
   - Platform compliance
   - Content guideline adherence

3. **Webhook Notifications**
   - New post alerts
   - Engagement milestones
   - Trending status
   - Safety warnings

#### Best Practices
1. **Content Optimization**
   - Trend alignment
   - Hashtag optimization
   - Post timing
   - Content categorization

2. **Growth Strategy**
   - Viral potential maximization
   - Engagement rate optimization
   - Follower retention
   - Content consistency

### Twitter
#### Overview
Rocket Social Boost provides comprehensive Twitter automation services with intelligent engagement distribution and natural growth patterns. The system supports both regular posts and retweets, with customized engagement patterns for each.

#### Features

##### Post Automation
- Automatic engagement on new tweets and retweets
- Smart distribution of likes, comments, views, and retweets over time
- Customized engagement patterns based on post type and package level
- Profile click integration for enhanced authenticity
- Bookmark automation for increased post visibility

##### Engagement Distribution
- Views: Multi-phase distribution (15-20%, 30-40%, 15-20%, 10-15% intervals)
- Likes: Distributed in small batches (10-17 per batch) over 30-hour periods
- Comments: AI-generated contextual comments based on post content and media
- Retweets: Natural distribution patterns with interval-based delivery
- Bookmarks: Strategic distribution to enhance post visibility

##### Safety Features
- Intelligent rate limiting and natural engagement patterns
- Automatic adjustment for retweet engagement (50% reduction)
- Profile protection through distributed engagement
- Customized timing for different engagement types

##### Package Types

###### Standard Package
- Base level engagement distribution
- Regular engagement patterns
- Standard comment generation
- Basic follower growth

###### Viral Package
- Enhanced engagement multipliers
- Accelerated distribution patterns
- Premium comment quality
- Aggressive follower growth
- Guaranteed minimum engagement levels

##### Engagement Heatmap

The system uses an intelligent time-based distribution system for engagement:

```
Hour (UTC) | Engagement Level
-----------+----------------
00-06      | 5-8%
06-12      | 10-15%
12-18      | 25-35%
18-24      | 15-25%
```

##### Commands

###### User Management
```
/twitter_lookup <username>
- Retrieves detailed user information
- Shows follower count, following count, and engagement metrics
- Displays profile information and statistics

/twitter_adduser <username> <package> <country> [email] [phone]
- Adds a user to the automation system
- Sets up package configuration
- Initializes engagement tracking
- Creates customer profile in the system
```

###### Post Management
```
/twitter_posts <username>
- Shows recent posts and their metrics
- Displays engagement statistics
- Provides post URLs and timestamps
```

###### Demo Features
```
/demotwitter <postlink> <package>
- Creates a demonstration of engagement features
- Shows real-time engagement distribution
- Displays cost calculations and timing
```

##### Best Practices

1. **Engagement Timing**
   - Allow 7-10 minutes before initial engagement
   - Distribute engagement over 30-hour periods
   - Use natural timing patterns for each engagement type

2. **Content Safety**
   - Automatic content type detection
   - Engagement adjustment for retweets
   - Profile protection measures

3. **Growth Patterns**
   - Natural follower growth distribution
   - Engagement based on account size
   - Progressive scaling of engagement

4. **Monitoring**
   - Real-time engagement tracking
   - Cost calculation and optimization
   - Performance metrics and analytics

### YouTube
- Video engagement automation
- View count management
- Like/dislike ratio control
- Comment generation and management
- Subscriber growth

### Google Business
- Review management
- Rating optimization
- Business profile engagement

## Task Scheduling System

The system uses two different task schedulers:

### New Scheduler (newchecker.py)
- Handles modern scheduling requirements
- Supports multiple order types
- Error handling and retry mechanisms
- Real-time status updates
- Webhook notifications for order status

### Legacy Scheduler (task_checker.py)
- Handles older scheduling patterns
- Basic scheduling functionality
- Simple retry mechanism
- Status tracking

## API Integrations

### Social Media APIs
- Instagram API (via RapidAPI)
- Twitter API
- LinkedIn API
- TikTok API
- YouTube API
- Google Business API

### Service APIs
- OpenAI API (for comment generation)
- Google Gemini API (for content analysis)
- Chargebee (for subscription management)
- FirstPromoter (for affiliate tracking)

### SMM Panel Integration
The system integrates with multiple SMM panels for service delivery:
- Just Another Panel
- More Than Panel
- Crescitaly
- OZ Social Market
- And many more...

## Commands

### General Commands
- `.sync` - Syncs the command tree
- `.exec` - Executes Python code (admin only)

### Moderation Commands
- `/ban` - Ban users
- `/kick` - Kick users
- `/purge` - Delete messages

### SMM Panel Commands
- `/order` - Place new order
- `/orderstatus` - Check order status
- `/panel_balance` - Check panel balance

## Security Notes

- API keys and tokens should be kept secure
- Proxy support is available for API calls
- Rate limiting is implemented for API calls
- Error handling and logging is in place

## Error Handling

The system includes comprehensive error handling:
- Discord webhook notifications for errors
- Logging to file system
- Retry mechanisms for failed orders
- Status tracking and monitoring

## Contributing

Please read CONTRIBUTING.md for details on our code of conduct and the process for submitting pull requests.

## License

This project is licensed under the MIT License - see the LICENSE.md file for details 
