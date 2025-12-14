> pip install dvc
> pip install "dvc[gdrive]"
> git init
> dvc init
> dvc add images
> git add images.dvc .gitignore
### git added the images folder to .gitignore
> git commit -m "added raw data"
> cat images.dvc
> tree ./.dvc/cache/

## dvc only keeps info about files, their locations and their hashes. But we also need to store these images somewhere. dvc doesnt store these images on its own, it only keeps track of it.
we need a storage for our data tracked by dvc. 

### specifying a storage for dvc
> dvc remote add -d <name-of-the-storage> <storage-uri>
example: dvc remote add -d gdrive gdrive://1_Wds-Ei_TibMKVTG-Er8H-ZObDq8HvIZ #the id if from drive url, value after folders/

next steps:

1. Open the correct Google Cloud project
Click this link (it already points to the right project):
👉 https://console.developers.google.com/apis/api/drive.googleapis.com/overview?project=365137703071
Or manually:
Google Cloud Console
Select project 365137703071
Step 2: Enable Google Drive API
Click Enable
Wait 1–2 minutes for propagation
-------

2. Create your own OAuth app in Google Cloud Console
Add yourself as a test user
Use your own client_id + client_secret

Use a Personal OAuth Client (Recommended for personal projects)
Go to the Google Cloud Console.
Create a new project (or use an existing one).
Navigate to APIs & Services → OAuth consent screen:
Choose External user type.
Fill in the required fields (app name, email, etc.).
Add scopes: https://www.googleapis.com/auth/drive and https://www.googleapis.com/auth/drive.appdata.
Save and publish the consent screen (for personal use, this doesn’t require verification).
Navigate to APIs & Services → Credentials → Create Credentials → OAuth client ID:
Application type: Desktop app.
Copy the Client ID and Client Secret.
Configure DVC to use this OAuth client ID:
dvc remote modify myremote gdrive_client_id <YOUR_CLIENT_ID>
dvc remote modify myremote gdrive_client_secret <YOUR_CLIENT_SECRET>
Run dvc push again — the browser prompt should now work without being blocked.

> dvc remote modify gdrive gdrive_client_id <client id>
> dvc remote modify gdrive gdrive_client_secret <client secret>
> dvc push

> rm -rf .dvc/cache # deleting the images in our cache
> rm -rf images # dvc is tracking so I dont need this folder images anymore in local
> dvc pull # images folder is back in local. Voila!

### When images folder is modified with new images
> dvc status
> dvc add images
> git status
> git add images.dvc
> git commit -m "updated my images"
> dvc push

> git log
> git checkout <commit hash>
> dvc pull # pulls images from that commit history
> git branch

#### add everything to gitrepo
> git remote add origin git@github.com:Varsha-Swaminathan/my_dvc_repo.git
> git branch -M main   
> git push -u origin main

> dvc config --list 
##### This command shows the final merged configuration that DVC is actually using (config + config.local together).

> list <repo url> <dir path>
