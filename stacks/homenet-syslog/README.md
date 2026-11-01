# Logging Stack

The central logging server for my homelab's network monitoring.

## Troubleshooting

Error:

```text
Your kernel does not support memory limit capabilities or the cgroup is not mounted. Limitation discarded.
```

Fix:

- Edit `/boot/firmware/cmdline.txt
- Add these params to the end of the existing line:
  
  ```text
  cgroup_enable=memory cgroup_memory=1
  ```

- Reboot to apply
