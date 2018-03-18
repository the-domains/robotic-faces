---
inFeed: true
description: Check out my A-start realisation for diagonal movement
dateModified: '2018-03-18T12:10:44.980Z'
datePublished: '2018-03-18T12:10:45.657Z'
title: ''
author: []
publisher: {}
via: {}
sourcePath: >-
  _posts/2018-03-18-check-out-my-a-start-realisation-for-diagonal-movementhttps.md
starred: false
datePublishedOriginal: '2018-03-18T12:04:37.219Z'
_type: Blurb

---
Check out my A-start realisation for diagonal movement

    def a_star(grid, h, start, goal):
        
        # TODO: Initialize the starting variables
        path = []
        queue = PriorityQueue()
        queue.put((0, start))
        # visited = set((0, start))
        visited = {}
        
        visited[start] = 0
        branch = {}
        found = False
        
        while not queue.empty():
            # TODO: Remove the first element from the queue
            item = queue.get()
            current_cost = item[0]
            current_node = item[1]
            
            # TODO: Check if the current vertex corresponds to the goal state
            # and set &grave;found&grave; to True if that's the case.
            if current_node == goal:        
                print('Found a path.')
                found = True
                break
            else:
                for action in valid_actions(grid, current_node):
                    # get the tuple representation
                    da = action.delta
                    cost = action.cost
                    next_node = (current_node[0] + da[0], current_node[1] + da[1])
                    # TODO: calculate new cost, c + g() + h()
                    new_cost = current_cost + cost + heuristic(next_node, goal)
                    
                    # TODO: Check if the new vertex has not been visited before.
                    # If the node has not been visited you will need to
                    # 1. Mark it as visited
                    # 2. Add it to the queue
                    if ((next_node not in visited) or 
                        (visited[next_node] > new_cost)):                
                        
                        visited[next_node] = new_cost
                        queue.put((new_cost, next_node))
                        
                        branch[next_node] = (new_cost, current_node, action)
        
        
        path = []
        path_cost = 0
        if found:
            
            # retrace steps
            path = []
            n = goal
            path_cost = branch[n][0]
            while branch[n][1] != start:
                # print("Current node:", n, sep=" ")
                # print("Prev node:", branch[n][1], sep=" ")
                path.append(branch[n][2])
                n = branch[n][1]
            path.append(branch[n][2])
                
        return path[::-1], path_cost

https://github.com/dambatenne/Flying\_cars/blob/master/A-Star.ipynb