# Daana authoring mechanics and applicability

Use this reference for model/mapping field choices and check boundaries. It is
tool-specific, not company-specific. Verify the selected compiler's vocabulary
and CLI support using the project's artifact/capability binding. These mechanisms
are not a guarantee across all Daana releases or generator modes. Source inspection
establishes implementation intent; execution and deployment need their own proof.

## Model fields and time

The typed-attribute DMDL vocabulary includes `STRING`, `NUMBER`, `UNIT`,
`START_TIMESTAMP` and `END_TIMESTAMP`. Use only the types actually supported by
the selected compiler. When `BOOLEAN` is unsupported, an explicitly defined
numeric 1/0 encoding is an owner-reviewed representation, not a new model type.

An attribute with `effective_timestamp: true` requests companion timestamp
storage. A mapping's `attribute_effective_timestamp_expression` requires that
model support; a checker may report `invalid-eff-tmstp-expression` otherwise.
Choose independent attribute time deliberately, not from a blanket true policy.
For compilers using grouped typed storage, a group permits at most one member per
storage type and the time declaration belongs to the group parent, not children.
Check generated fields/checker behavior when the compiler changes.

`allow_multiple_identifiers` is a mapping-group identity policy, not a model field
or compound-key shortcut. Collision handling, load order and reversibility remain
separate design/proof requirements. Place relationships at the compiler-supported
mapping-group level; accepted unknown or table-level fields may be ignored.

## Structural check boundaries

Bind the installed binary, explicit config and model/mapping/workflow paths before
forming commands. On CLIs exposing these options, `check model` is structural,
`check mapping --skip-schema-validation` avoids warehouse schema access, and
`check workflow` without `--source` avoids source validation. Confirm help/code
on the actual artifact; these are not universal safe invocations based on names.
Connected checks are a different authorized operation. Where connection failures
are warnings by default, select the supported strict failure mode and inspect
results. Neither offline warnings nor a zero exit status prove source access.

Static validation has blind spots to test by mechanism: target identifier type
mismatch; analytic expressions inserted in scalar/WHERE context; unknown YAML
ignored rather than rejected; relationship stanzas accepted but not generated.
Inspect complete generated output and evaluate the relevant context. Read the
project's dated evidence for which issues were source-inspected, synthetically
executed or observed in deployment; do not claim all four were reproduced.

Deploy creates structure before execute can populate a new attribute. Whether
initial execute backfills and which refresh levels clear history are properties
of the selected artifact, not reasons to request an automatic full refresh.
Use the operations and verification skills for those separate tasks.
