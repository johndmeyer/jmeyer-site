* docker `build -t jmeyer-site-image .`
* docker `run --name jmeyer-site-container -p 80:80 jmeyer-site-image`
    * ensure app runs as expected locally

* goto google cloud artifact registry - create registry (if not already existing)

* `/Volumes/OS/Users/johndmeyer/google-cloud-sdk/bin/gcloud init`
* `/Volumes/OS/Users/johndmeyer/google-cloud-sdk/bin/gcloud auth login`
* `/Volumes/OS/Users/johndmeyer/google-cloud-sdk/bin/gcloud auth configure-docker us-central1-docker.pkg.dev`
* `docker tag jmeyer-site-image us-central1-docker.pkg.dev/fluid-axe-449221-n2/jmeyer-site/jmeyer-site-image`
* `docker push us-central1-docker.pkg.dev/fluid-axe-449221-n2/jmeyer-site/jmeyer-site-image`

* Go back to the google cloud console and go to cloud run
* Click 'Deploy Container' => Service
* Select the image from artifact registry and fill in the form with the appropriate configs
    * Nice video here https://www.youtube.com/watch?v=MM4viHa7k4w
* Map domain name to google ips - this was a bit tricky but shouldn't need to be done again

** To deploy a new image **
* Follow steps above to upload the image to artifact registry
* Goto cloud run in the google cloud console at choose the existing service `jmeyer-site-image` TODO: rename this...
* Click 'Edit & Deploy New Revision' at the top of the page
* Choose the new image we just uploaded