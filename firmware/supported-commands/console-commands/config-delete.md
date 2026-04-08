# config-delete

Removes a single configuration key from a config file. This is complementary to **`config-set`** (which adds or overwrites a key).

### Usage

```
config-delete sd <configuration_setting_key>
```

* **configuration_setting** — the dotted key to remove (same style as `config-get` / `config-set`).

On success, the console reports that the setting was removed. If the key is missing or the source is read-only, the command reports **not found** or **read-only**.


