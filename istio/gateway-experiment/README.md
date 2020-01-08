# Gateway - Fashion latency chaos experiment

|                        |                                                                                                        |
| ---------------------- | ------------------------------------------------------------------------------------------------------ |
| Hypothesis             | When our Fashion service has a high delay, the Gateway service will still respond in less than 250 ms. |
| Classification         | reliability, usability                                                                                 |
| Target                 | Gateway service                                                                                        |
| Attack Type            | Latency Attack                                                                                         |
| Blast Radius           | Gateway service & Fashion service                                                                      |
| Steady State Defintion | The gateway service responds in <= 250 ms.                                                             |
| Steady State before    | *Fill out when running the experiment*                                                                 |
| Steady State during    | *Fill out when running the experiment*                                                                 |
| Steady State after     | *Fill out when running the experiment*                                                                 |
| Findings               | *Fill out when running the experiment*                                                                 |

## Prerequisites

- Prerequisites of shopping demo (see README at root)
- Installed [JMeter](https://jmeter.apache.org/)

## How to run

1. Apply 250 ms timeout for fashion service  
`kubectl apply -f ./01-fashion-vs-timeout.yaml`
2. Generate basic load to monitor steady state  
`jmeter -n -t istio/gateway-experiment/load-generator.jmx`

### Using Istio failure injection via VirtualService

> This approach does not work in combination with VirtualService timeout configuration.

```bash
kubectl apply -f ./02-fashion-vs-timeout-and-failure.yaml
```

### Using Istio failure injection via EnvoyFilter

> This approach works in combination with VirtualService timeout configuration

```bash
kubectl apply -f ./03-fashion-sidecar-inbound.yaml
```
