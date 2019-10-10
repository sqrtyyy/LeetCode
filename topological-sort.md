# Topological-sort

+ [Course Schedule](#course-schedule)
+ [Course Schedule II](#course-schedule-ii)
+ [Alien Dictionary](#alien-dictionary)

# Course Schedule

https://leetcode.com/problems/course-schedule/

```C++
class Solution {
public:
    bool DeepFirstSearch(int course,  vector<vector<int>>& courseTakes, vector<bool>& completedCourses, vector<bool>& usedCourses){
        int succeed = 0;
        usedCourses[course] = true;
        for(auto reqCourse : courseTakes[course]){
            if(!completedCourses[reqCourse]){
                if(usedCourses[reqCourse])
                    break;
                if(DeepFirstSearch(reqCourse, courseTakes, completedCourses, usedCourses))
                   completedCourses[reqCourse] = true;  
            }
            if(completedCourses[reqCourse])
                succeed++;
        }
        return succeed == courseTakes[course].size();
    }
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        vector <vector<int>> courseTakes(numCourses);
        vector <bool> completedCourses(numCourses, false);
        for(auto pair : prerequisites)
            courseTakes[pair[0]].push_back(pair[1]);   
        for(int i = 0; i < numCourses; i++){
            vector <bool> usedCourses(numCourses, false);
            if(!completedCourses[i])
                if(!DeepFirstSearch(i, courseTakes, completedCourses, usedCourses))
                    return false;
        }
        return true;
    }

};
```

# Course Schedule II

https://leetcode.com/problems/course-schedule-ii/

```C++
class Solution {
public:
    bool DeepFirstSearch(int course,  vector<vector<int>>& courseTakes, vector<bool>& completedCourses, vector<bool>& usedCourses, vector<int>& order){
        if(completedCourses[course])
            return true;
        
        int succeed = 0;
        usedCourses[course] = true;
        for(auto reqCourse : courseTakes[course]){
            if(!completedCourses[reqCourse]){
                if(usedCourses[reqCourse])
                    return {};
                if(DeepFirstSearch(reqCourse, courseTakes, completedCourses, usedCourses, order))
                    completedCourses[reqCourse] = true;
            }
            if(completedCourses[reqCourse])
                succeed++;
        }
        order.push_back(course);
        if(succeed == courseTakes[course].size())
            completedCourses[course] = true;
        return succeed == courseTakes[course].size();
    }
    vector <int> findOrder(int numCourses, vector<vector<int>>& prerequisites) {
        vector <int> order;
        vector <vector<int>> courseTakes(numCourses);
        vector <bool> completedCourses(numCourses, false);
        for(auto pair : prerequisites)
            courseTakes[pair[0]].push_back(pair[1]);   
        for(int i = 0; i < numCourses; i++){
            vector <bool> usedCourses(numCourses, false);
            if(!completedCourses[i])
                if(!DeepFirstSearch(i, courseTakes, completedCourses, usedCourses, order))
                   return {};
        }
        return order;
    }

};
```
