# spring-hello-notes

Reset Instructions
------------------
Delete source code directory
Delete previously deployed hello app on PWS through apps manager


Describe PWS environment

Show Apps Manager UI: https://console.run.pivotal.io/

Login from command line:

```
cf login
```

Ready to get started with the Spring Initializr: https://start.spring.io/

Switch to gradle

Group: com.springdev.demo

Artifact: hello

Click Generate Project

Go to workspace in terminal:

```
mv ~/Downloads/hello.zip .
unzip hello.zip
```

Add a hello REST endpoint to our microservice:

```
	@RestController
	class HelloController {
		@GetMapping("/hello")
		String hello() {
			return "Hello from PAS!";
		}
	}
```

Modify the application.properties file to expose the Actuator endpoints:

```
management.security.enabled=false
management.endpoints.web.exposure.include=*
endpoints.env.enabled=true
```

Now lets create a manifest.yml file to make our cf push CLI commands a little cleaner:

manifest.yml
```
---
applications:
- name: <insert appname here>
  instances: 1
  memory: 750MB
  routes:
  - route: <insert appname here>.cfapps.io
  stack: cflinuxfs3
```

We are now ready to push our sample application. The gradle build will generate an executable JAR fort us that we will deploy.

```
./gradlew build
cf push -p build/libs/hello-0.0.1-SNAPSHOT.jar
```

Explain the buildpack interrogation and that you can simply specify what buildpack to use to speed things up.

Show app deployed in apps manager and launch.

Add /hello to hit our REST endpoint we defined

Show actuator endpoints: actuator/{env, metrics, health}

Examine app in Apps Manager on PWS

Show how health checks get pulled in, logs, and metrics become available by default




