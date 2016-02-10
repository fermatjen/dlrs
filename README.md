# DLRS
DLRS (Distributed Learning Record Store) allows you to quickly record and retrieve discreet user activities. DLRS is anything but an LRS (Learning Record Store) but both have some features in common. DLRS is not written conforming to the LRS specification so obviously won't work with applications supporting the xAPI/LRS. DLRS was quickly written to act as a dandy and lightweight LRS that you can use as a record store to store all user activities.

This software is still under development. Don't even think of using it.

To build a JAR from the sources, run:

```
$ gradle assemble
```
You will find the JAR file from the libs dir.

To test DLRS, directly run:

```
$ ./gradlew run
```
When the DLRS server is running, open the following page to test:

```
http://localhost:8678/learn
```
# API Usage
DLRS exposes a few endpoints for your apps to store and retrieve atomic user activities. Every 'measurable' user activity is represented by a 'Statement' or action. 

A 'Statement' can be sent to a DLRS with 3 primary payload details:

* *Actor* - Who is this user?
* *Verb* - What did he do?
* *Object* - What is he learning?

## To record a statement
Send a POST request

```http
POST /learn/statement
```
with the following JSON request body:

```json
{
    "actor": {
        "objectType": "User",
        "name": "Abel Osbert",
        "mbox": "mailto:aosbert@example.com"
    },
    "verb": {
        "id": "http://adlnet.gov/expapi/verbs/completed",
        "display": {
            "en-US": "completed"
        }
    },
    "object": {
        "objectType": "Activity",
        "id": "http://www.example.com/activities/001",
        "definition": {
            "name": {
                "en-US": "Example Activity"
            },
            "type": "http://adlnet.gov/expapi/activities/course"
        }
    }
}
```
