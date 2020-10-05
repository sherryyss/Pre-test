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

#### get(key):

if key not in the cache:

    return -1

else:

use the current time to calculate the weight, since the last access time and current time is same in this case we can use this formula to update the weight of the given key:


   calc_weight = key score / math.log(time.time())
   
   self.key_scores[key] = calc_weight
   
   return cache[key]
   

The best case and average case time complexity of get(key) function is O(1) since we are using a dictionary as our data structure and it has O(1) access time


  
#### put(key, value, weight):

first time key is placed in cache let's use the given formula to assign it a key: 

   calc_weight = weight / 100
  
  
   if key not in the cache:
   
      if cache is full: 
      
         search key_scores to get the lowest scored key 
         
         one found, remove the lowest scored key from cache and from key_scores
         
         now we can add the new entry in cache along with its score in key_scores
         
      else:
      
         cache is not full so we just need to add the new entry in cache along with its score in key_scores

least_scored() => To implement the search, we place all the weights in a list() first and apply a sort to get the lowest weight first. Given the lowest weight, get the first corresponding key having the given weight. This is the key that will be removed.


The worst case time complexity of put(key, value, weight) function is O(n) because we have to traverse through the key_scores dictionary to find the element with the minimum score. 
