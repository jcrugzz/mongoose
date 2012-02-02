## Model.update

Updates all documents matching `conditions` using the `update` clause. All `update` values are casted to their appropriate types before being sent.

    var conditions = { name: 'borne' }
      , update = { $inc: { visits: 1 }}
      , options = { multi: true };

    Model.update(conditions, update, options, callback)

Keep in mind that that the `safe` option specified in your schema is used by default when not specified here.

Note: for backwards compatibility, all top-level `update` keys that are not $atomic operation names are treated as `$set` operations. Example:

    var query = { name: 'borne' };
    Model.update(query, { name: 'jason borne' }, options, callback)

    // is sent as

    Model.update(query, { $set: { name: 'jason borne' }}, options, callback)

This helps prevent accidentally overwriting all of your document(s) with `{ name: 'jason borne' }`.