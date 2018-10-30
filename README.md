# Google Cloud Functions Demo

**Simple tutorial for Google Cloud Functions**

To follow along in this demo, you'll need to register for a GCP account, for which you need a creditcard, on first use of GCP you get $300 worth of credits, to test-drive payed features. The demo as such should not cost anything, but there are no guarantees this is still correct when you follow this tutorial, do procede at your own risk. Also sometimes an API needs to be activated for certain services, in this tutorial all API's will be enabled by following the command prompt in the cloud shell. So don't get distracted by messages in the main cloud console screen, just read the instructions and answer yes when prompted to enable the API.
 
Start your Google Cloud Console, open the Cloud Shell command-prompt (depicted by small icon `>_` at the top of the GCP interface), from the console (black and white window at the bottom of your screen) envoke following command to creat a directory:

`mkdir ~/gcf_http`

and then change into the directory:

`cd ~/gcf_http`

Then create a file index.js and copy the contents bellow into it:

`nano index.js`

copy (CTRL-C, CRTL-V) text below, CTRL-X to close answer Y to save the file.


```javascript
/**
 * Responds to any HTTP request that can provide a "message" field in the body.
 *
 * @param {!Object} req Cloud Function request context.
 * @param {!Object} res Cloud Function response context.
 */
exports.helloWorld = (req, res) => {
  // Example input: {"message": "Hello!"}
  if (req.body.message === undefined) {
    // This is an error case, as "message" is required.
    res.status(400).send('No message defined!');
  } else {
    // Everything is okay.
    console.log(req.body.message);
    res.status(200).send('Success: ' + req.body.message);
  }
};
```

Run the command bellow to deploy the index.js as a function called helloWorld, of the type "trigger-http", during the setup you could be prompted to enable the API, answer with y and continue:

`gcloud beta functions deploy helloWorld --trigger-http`

Once the function is deployed you need to find the trigger URL in the returned statement "httpsTrigger:" and use it to build the follwing command to envoke the trigger:

`curl -H "Content-Type:application/json" -d '{"message":"Hello TedQ World!"}' "https://[YOUR_HTTPS_Trigger]"`

Alternativly you can find the URL by going into the Google Cloud Functions dashboard and select trigger tab and find the URL:

![image](https://raw.githubusercontent.com/quintest/tedq/master/Aantekening%20(15).png)


This should return the following statement:

`"Success: Hello TedQ World!"`

After your done testing the function type:

`gcloud beta functions delete helloWorld`

and follow the instructions on screen.

*Source of the index.js file is the default helloWorld function which gets deployed when you create your first function on Google Cloud Function.*
