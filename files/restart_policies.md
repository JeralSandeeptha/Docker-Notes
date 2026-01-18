# Restart Policies
- Restart policies help ensure your containers automatically restart under certain conditions (like after a crash or reboot)

## ✅ Common Restart Policies
| Policy                     | Behavior                                                                 |
| -------------------------- | ------------------------------------------------------------------------ |
| `no` (default)             | Do not restart                                                           |
| `always`                   | Always restart the container no matter what                              |
| `unless-stopped`           | Restart always except when explicitly stopped by user                    |
| `on-failure[:max-retries]` | Restart only if the container exits with a non-zero status (e.g., crash) |

```cmd
docker run --restart=unless-stopped myapp
```
