# Priority

Priority allows independent gameplay systems to request outlines on the same actor without directly coordinating with one another.

Higher priority values take precedence over lower priority values.

## Example

| Request | Priority |
| --- | ---: |
| Interaction | 10 |
| Objective | 50 |
| Critical Target | 100 |

If all three requests are active, the Critical Target request takes precedence.

When the winning request is removed or expires, the remaining active requests can be resolved according to priority.

## Recommended Practice

Leave gaps between priority values, for example `10`, `20`, `50`, `100`. This makes future presets easier to insert.
