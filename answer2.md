### Answer 2:

```Python
import math
import time

class Cache: 

    def __init__(self, capacity):
        self.cache_capacity = capacity
        self.cache = dict()
        self.key_scores = dict()
              
    def is_cache_full(self):
        return len(self.cache) == self.cache_capacity 
      
    def get(self, key):
        if key not in self.cache:
            return -1
        else:
            calc_weight = self.key_scores[key] / math.log(time.time())
            self.key_scores[key] = calc_weight
            return self.cache[key]
      
    def least_scored(self):
        key_scores_list = list(self.key_scores.values())
        key_scores_list.sort()
        
        for key, val in self.key_scores.items():
            if val == key_scores_list[0]:
                return key
            
       
    def put(self, key, value, weight):
        calc_weight = weight / 100
        
        if key not in self.cache:
            if self.is_cache_full(): 
                # remove lowest scored key from cache and from key_scores
                least_scored_key = self.least_scored()
                self.cache.pop(least_scored_key)
                self.key_scores.pop(least_scored_key)
                # add entry in cache and key_scores so we can keep track of least scored key
                self.key_scores[key] = calc_weight
                self.cache[key] = value 
            else:
                self.key_scores[key] = calc_weight
                self.cache[key] = value
                    

cache2 = Cache(2)

cache2.put("key", 1, 1)
cache2.put("key1", 1, 16)
cache2.put("key2", 1, 20)

print(cache2.get("key2"))
```

