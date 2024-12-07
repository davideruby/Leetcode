## [743. Network Delay Time](https://leetcode.com/problems/network-delay-time/)

${\textsf{\color{yellow}Medium}}$

You are given a network of n nodes, labeled from 1 to n. You are also given times, a list of travel times as directed edges times[i] = (ui, vi, wi), where ui is the source node, vi is the target node, and wi is the time it takes for a signal to travel from source to target.

We will send a signal from a given node k. Return the minimum time it takes for all the n nodes to receive the signal. If it is impossible for all the n nodes to receive the signal, return -1.

## Solution
```python
import heapq
class Solution:
    def networkDelayTime(self, times: List[List[int]], n: int, k: int) -> int:
        graph = self.buildGraph(times, n)
        delays = {node: float("inf") for node in graph.keys()}
        delays[k] = 0
        heap = [(0, k)]
        
        while heap:
            delay_from_start, node = heapq.heappop(heap)

            for neighbor, weight in graph[node].items():
                new_delay = weight + delay_from_start
                if new_delay < delays[neighbor]:
                    delays[neighbor] = new_delay
                    heapq.heappush(heap, (new_delay, neighbor))

        network_delay = max(delays.values())
        return network_delay if network_delay != float("inf") else -1

    
    def buildGraph(self, times, n):
        graph = {node: {} for node in range(1, n + 1)}

        for src, dest, weight in times:
            graph[src][dest] = weight

        return graph
```

## Notes
Simply return max from distance array of dijkstra and if anyone is infinite then give -1.
