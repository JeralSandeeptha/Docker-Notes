# Resource Management
- Docker lets you limit and control the amount of system `resources` (`CPU`, `memory`, etc.) your containers use. This is helpful when running multiple containers or on shared infrastructure.
- We can identify 3 resources in docker container
 - `CPU`
 - `Memory`
 - `Network`

- If you want to get quick details
```cmd
docker stats
```

- Common Resource Constraints

| Resource       | Flag                                      | Example                          | Description                          |
| -------------- | ----------------------------------------- | -------------------------------- | ------------------------------------ |
| **Memory**     | `--memory` or `-m`                        | `-m 512m`                        | Limits memory to 512MB               |
| **CPU shares** | `--cpu-shares`                            | `--cpu-shares 512`               | Relative weight; default is 1024     |
| **CPU quota**  | `--cpu-quota`                             | `--cpu-quota=50000`              | Microseconds of CPU time allowed     |
| **CPU period** | `--cpu-period`                            | `--cpu-period=100000`            | Period for CPU quota (default 100ms) |
| **CPU limit**  | `--cpus`                                  | `--cpus="1.5"`                   | Set number of CPUs directly          |
| **PIDs limit** | `--pids-limit`                            | `--pids-limit=100`               | Limit number of processes            |
| **Disk I/O**   | `--device-read-bps`, `--device-write-bps` | `--device-read-bps=/dev/sda:1mb` | Limit disk I/O bandwidth             |

<br />

## CPU
-  This allows you to control how much CPU power your containers use, which is vital when running multiple containers or optimizing performance.

- Why Manage CPU in Docker?
 - Prevent one container from hogging all the CPU.
 - Ensure fair CPU usage across multiple containers.
 - Simulate CPU limits for testing or production constraints.

- `--cpus` – Limit CPU cores directly
```bash
// ✅ This means the container can use up to 1.5 CPU cores.
docker run --cpus="1.5" myapp
```

- `--cpu-shares` – Set relative CPU priority
```bash
docker run --cpu-shares=512 myapp

/*
Default is 1024.
It’s not a hard limit, but a weight.
If two containers are running:
 One has 1024, the other 512
 The first gets twice as much CPU time as the second.
✅ Useful when all containers compete for CPU.
*/
```

- `--cpu-quota` and `--cpu-period` – Fine-grained control
```bash
docker run --cpu-quota=50000 --cpu-period=100000 myapp

/*
This allows the container to use 50% of a single CPU.
Formula: quota / period = CPU usage
Default period is 100000 µs (100 ms)
✅ Useful when you want precise CPU limits, especially for high-density setups.
*/
```

- `--cpuset-cpus` – Pin container to specific CPU cores
```bash
docker run --cpuset-cpus="0,2" myapp

/*
✅ This forces the container to run only on CPU 0 and 2.

✅ Good for:
Performance isolation
Real-time or latency-sensitive apps
*/
```

<br />

## Memory
- An essential topic for running containers efficiently and avoiding crashes due to memory overuse.

- By default, Docker containers can use all available system memory, which can lead to:
 - Memory exhaustion on the host
 - One container killing others (via OOM – Out Of Memory)
 - Performance bottlenecks

- `--memory` or `-m` → Set max memory limit
```bash
docker run -m 512m nginx

/*
This limits the container to 512MB of RAM.

You can also use:
 k (kilobytes)
 m (megabytes)
 g (gigabytes)
*/
```

- `--memory-swap` → Set total memory + swap
```bash
docker run -m 512m --memory-swap 1g nginx

/*
This means:
512MB RAM

512MB swap (total: 1GB memory usage allowed)
🧠 Swap is slower than RAM and is used when memory runs out.
*/
```

- `--memory-reservation` → Soft limit (ideal usage)
```bash
docker run --memory-reservation=300m -m 512m nginx

/*
If under 300MB → container runs smoothly.
If memory pressure occurs → Docker tries to keep it under 300MB.
Hard limit remains 512MB.
*/
```

- `--oom-kill-disable` → Prevent auto-killing
```bash
docker run -m 512m --oom-kill-disable nginx

/*
Disables Docker's Out Of Memory killer, which normally kills containers that exceed memory.
⚠️ Use carefully — container may hang instead of being killed.
*/
```

- `--kernel-memory` (Deprecated in newer Docker versions) - (Deprecated)

<br />

## Network
- Docker uses network drivers to enable communication between containers, host, and the outside world
![Image](https://res.cloudinary.com/djgwvmcdl/image/upload/v1751199734/6_bro6yv.png)
