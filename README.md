# issue-meteor-11666
Exploration of solutions for issue #11666 in the Meteor repository.

## Example errors

Source: https://github.com/meteor/meteor/issues/11666#issuecomment-1037334159

- context: Meteor server error
- type: `MongoServerError`
- message: `An equivalent index already exists with the same name but different options. Requested index: <...>, existing index: <...>`
- code: `85`
- codeName: `"IndexOptionsConflict"` 
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

---

Source: https://github.com/meteor/meteor/issues/11750#issue-1046122141

- context: Mongo server error
- message: "Index with name: emails.address_1 already exists with different options"
- code: `85`
- codeName: `"IndexOptionsConflict"` 
