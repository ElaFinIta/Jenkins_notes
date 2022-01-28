# CI, Continuous Integration: Jenkins notes >>> making a Pipeline

0. In Jenkins you should have installed nodejs, (Pipeline, Blue Ocean, Docker Pipeline) plugin (Dashboard> Manage plugins)
1. In your multiple branch repo project folder, make a Jenkins file named `Jenkinsfile` with no extension (you can also put the script directly in the later configuration)

```sh
pipeline {
    agent any 

    stages {

        stage ("Test") {
            steps {
                echo 'Echoing fake testing, nothing really happening...'
            }
        }
        stage ("Build") {
            steps {
                echo 'Wanna-be building of the app'
            }
        }
        stage ("Delpoy") {
            steps {
                echo 'Deploying in fantasy world'
            }
        }
    }
} 
```

2. From Docker (don't sign-in) , start Jenkins (press play)
3. When container is running, go to localhost:8080 in browser to see UI (default port for jenkins is 5000)
4. NEW ITEM to make a new Pipeline, specify a name and choose either Pipeline or Multibranch Pipeline (if you want to detect multiple branches of your repo)
5. add display name and source, ex. github repo url (add directly pipeline script if you don't have a Jenkinsfile in the project). In case of multiple branches, add source for all of them >>> discover all branches
6. DONE
![main_branch_ok](https://user-images.githubusercontent.com/88823568/151505511-3d2809d8-be47-40d9-abc3-7a63cc00d257.png)

7. Try to break it from another branch >>> git checkout -b my-new-branch-name >>> break the Jenkinsfile by omitting a stage, for example:
```sh
pipeline {
    agent any 

    stages {

        stage ("Test") {
            steps {
                echo 'Echoing fake testing, nothing really happening...'
            }
        }
                       {
            steps {
                echo 'Wanna-be building of the app'
            }
        }
        stage ("Delpoy") {
            steps {
                echo 'Deploying in fantasy world'
            }
        }
    }
} 
```

9. After pushing you'll see that the pipeline broke:


![broken_pipeline](https://user-images.githubusercontent.com/88823568/151505753-a3ba656a-7c2e-42bb-8146-19ef71b92976.png)


This is the view with the Blue Ocean plugin:

![blue_ocean](https://user-images.githubusercontent.com/88823568/151505815-001b2b2c-1250-4c72-adb5-f49f58c70034.png)
![blue_ocean2](https://user-images.githubusercontent.com/88823568/151506112-e0f9d586-87fb-4ec5-b51e-2584382a17a8.png)

10. Revert the mistake by fixing the Jenkinsfile >>> after pushing, the pipeline of both branches are ok
![success](https://user-images.githubusercontent.com/88823568/151506191-7bd6924e-bbc5-462a-8b39-b6e16157d936.png)

![blueocean_success](https://user-images.githubusercontent.com/88823568/151506665-0d3fcc03-3a56-4924-8bd7-644f2f16f516.png)

