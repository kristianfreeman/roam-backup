# [[`roam-backup`]]

Automate backing up JSON copies of your [Roam Research](https://roamresearch.com) data, using GitHub Actions and AWS S3.

Backups will be generated using Puppeteer and saved into the `backups` folder (`config.backupFolder`, can be changed) of an S3 bucket of your choice.

## Usage

You can get `roam-backup` up and running in just a few minutes! The best part is that **you don't need to deploy anything!** 

Just follow these steps and you'll be on your way:

1. Fork this repository.
2. Enable Actions on the repository, as they get disabled upon forking.
3. Setup an AWS S3 bucket to store your Roam backups:

- Ensure you create the AWS S3 bucket manually –– this script will not create the bucket. Note the `awsBucketName` for step #4.
- Create (or reuse) a user in the AWS console, and ensure it has permissions to upload to an S3 bucket (the `S3FullAccess` policy will guarantee it, but you can use a more conservative policy that simply enables upload). Note the `awsAccessKeyId` and `awsAccessKeySecret` of the user for step #4.

4. In your Github repository's Settings, go to the Secrets section and add the following secrets (**naming must match exactly!**):

- `roamEmail`
- `roamPassword`
- `awsBucketName`
- `awsAccessKeyId`
- `awsAccessKeySecret`

_Don't worry! Your Roam and AWS credentials will be secure. GitHub [Secrets](https://help.github.com/en/actions/configuring-and-managing-workflows/creating-and-storing-encrypted-secrets) are encrypted, and provide a convenient methodology for storing secure data in repositories._

5. Make a commit. It can be any commit, but this will start the process and trigger workflows.

Congrats! 🎉 You've successfully automated the backup of your brain 🧠. Now go write about it in today's Daily Note!

_NOTE: This is still fairly WIP, and this is my first project using Puppeteer, so it may be a little buggy._

## Development

Running this project locally should be possible using `.env` - copy `.env.example` to `.env` and fill it in with your own authentication keys. 

The project generates an `error.png` screenshot to capture the current page if something goes wrong, as well as ZIP folders, which are the JSON backups. Running `npm start` will clear any local screenshots and backups, and run the script as it would in the GitHub Actions workflow (`npm start`)
