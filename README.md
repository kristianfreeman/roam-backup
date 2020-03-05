`roam-backup`

Automate backing up JSON copies of your [Roam Research](https://roamresearch.com) data, using GitHub Actions and AWS S3.

Backups will be generated using Puppeteer and saved into the `backups` folder (`config.backupFolder`, can be changed) of an S3 bucket of your choice.

## Usage

To use it, just fork this repo and add the following [secrets](https://help.github.com/en/actions/configuring-and-managing-workflows/creating-and-storing-encrypted-secrets) to your repo (naming must match!):

- roamEmail 
- roamPassword
- awsBucketName
- awsAccessKeyId
- awsAccessKeySecret

AWS/S3 notes: the user that is represented by these access keys should have permissions to upload to an S3 bucket. I use `S3FullAccess` - if there's something else I should use, please let me know/open a PR to correct this README. The S3 bucket that the backups will upload to should already be created: this script won't create the bucket for you.

This is still fairly WIP, and this is my first project using Puppeteer, so it may be a little buggy.

## Development

Running this project locally should be possible using `.env` - copy `.env.example` to `.env` and fill it in with your own authentication keys. 

The project generates an `error.png` screenshot to capture the current page if something goes wrong, as well as ZIP folders, which are the JSON backups. Running `npm start` will clear any local screenshots and backups, and run the script as it would in the GitHub Actions workflow (`npm start`)
