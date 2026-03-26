# homedemo-setup
Combination of different demo's, show and tells that I need now organized into one location.


`/cluster` contains the app that sets what cluster-day2 configuration shoudl be applied

`/cluster-day2` contains day 2 configurations (these are configs that are outside of and prior to any demo)

`/infa` primarily things like argo and security around that needed that the cluster needs prior also keycloak with oauth that sorta thing

`/demo-dep` this is going to container operators and direct independent components that are actually dependencies pulled in for a specific demo, perhaps special configs around a particular setup config

`/live/demos/` the actual demo, which will pull in `/demo-dep`'s and additional files, something like this demo needs operator a, b, c and then the actual demo material

`/live` which operators or demos are to be pulled in technicall should be overlays but its just e so meh

