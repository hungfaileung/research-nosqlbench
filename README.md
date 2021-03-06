# research-nosqlbench

- <https://docs.nosqlbench.io/#/docs/>
- <https://github.com/nosqlbench/nosqlbench>

## Resources

- Benchmark your NoSQL Database
  - nice workshop
  - <https://www.youtube.com/watch?v=rLx2uJCeJKk>
  - <https://github.com/DataStax-Academy/nosqlbench-workshop-online>

- NoSQLBench demo - Designing Test Workloads | David Joy 
  - talking about the yaml file
  - <https://www.youtube.com/watch?v=jHZeGy_ZHcU>
  - <https://github.com/david-joy-ds/NosqlBench>

- #7 Testing your Application
  - same materials as "Benchmark your NoSQL Database", but different speakers
  - <https://www.youtube.com/watch?v=rcyetfquNq4>

## Firestore Testing

- <https://cloud.google.com/firestore/docs/use-rest-api>
- <https://developers.google.com/identity/protocols/oauth2/service-account#httprest>
- <https://developers.google.com/spectrum-access-system/guides/authorization-and-authentication>
- <https://cloud.google.com/firestore/docs/reference/rest/v1/projects.databases.documents/createDocument>

```
  curl --request POST \
  'https://firestore.googleapis.com/v1/projects/sixth-storm-328014/databases/(default)/documents/users?documentId=testgarydoc01' \
  --header 'Authorization: Bearer [your token]' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --data '{"fields":{"name":{"stringValue":"gary"}}}' \
  --compressed
```

```
java -jar nb.jar run driver=http workload=test.yaml cycles=2
```

- test.yaml
```
statements:
    - testing:
      method: 'POST'
      uri: 'https://firestore.googleapis.com/v1/projects/sixth-storm-328014/databases/(default)/documents/users?documentId=testgary'
      Content-Type: 'application/json'
      Authorization: 'Bearer [your token]'
      body: '{"fields":{"name":{"stringValue":"gary"}}}'
```




```
java -jar nb.jar run driver=http workload=test.yaml cycles=10000 threads=auto
```

```
statements:
    - testing:
      method: 'POST'
      uri: 'https://firestore.googleapis.com/v1/projects/[your project]/databases/(default)/documents/users?documentId=testgary{alpha}'
      Content-Type: 'application/json'
      Authorization: 'Bearer [your token]'
      body: '{"fields":{"name":{"stringValue":"gary{alpha}" }}}'
bindings:
 alpha: Identity()
 beta: NumberNameToString()
 gamma: Combinations('0-9A-F;0-9;A-Z;_;p;r;o;')
 delta: WeightedStrings('one:1;six:6;three:3;')
```
