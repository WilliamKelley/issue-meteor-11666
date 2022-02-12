# issue-meteor-11666
Exploration of solutions for issue #11666 in the Meteor repository.

## Example errors

From user @champel in issue [comment](https://github.com/meteor/meteor/issues/11666#issuecomment-1037334159)

- main message: `MongoServerError: An equivalent index already exists with the same name but different options. Requested index: <...>, existing index: <...>`
- error properties: 
  - `"code": 85`, 
  - `"codeName": 'IndexOptionsConflict'`
- requested index:

```json
{
  "v": 2,
  "key": { "services.resume.haveLoginTokensToDelete": 1 },
  "name": "services.resume.haveLoginTokensToDelete_1",
  "sparse": true
}
```

- existing index:

```json
{
  "v": 2,
  "key": { "services.resume.haveLoginTokensToDelete": 1 },
  "name": "services.resume.haveLoginTokensToDelete_1",
  "sparse": 1
}
```

Difference: requesting `"sparse": true` is incompatible with existing `"sparse": 1`.
