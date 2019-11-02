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
## Alien Dictionary

https://www.lintcode.com/problem/alien-dictionary/description

```C++
class Solution {
public:
     void BuildGraph(vector<string> &words, vector<vector<int>>& graph){
        for(int i = 1; i < words.size(); i++){
            string word_1 = words[i];
            string word_2 = words[i - 1];
            int length = min(word_1.length(), word_2.length());
            for(int j = 0; j < length; j++){
                if(word_1[j] != word_2[j]){
                    graph[word_1[j] - 'a'].push_back(word_2[j] - 'a');
                    break;
                }
            }
        }
        
     }
     bool DeepFirstSearch(int letter, vector<vector<int>>& graph, vector<bool>& completedLetters, vector<bool>& usedLetters, string& order){
        if(completedLetters[letter])
            return true;
        int succeed = 0;
        usedLetters[letter] = true;
        for(auto reqletter : graph[letter]){
            if(!completedLetters[reqletter]){
                if(usedLetters[reqletter])
                    return {};
                if(DeepFirstSearch(reqletter, graph, completedLetters, usedLetters, order))
                    completedLetters[reqletter] = true;
            }
            if(completedLetters[reqletter])
                succeed++;
        }
        order.push_back(letter + 'a');
        if(succeed == graph[letter].size())
            completedLetters[letter] = true;
        return succeed == graph[letter].size();
    }
    string alienOrder(vector<string> &words) {
        bool letters[26] = {0};
        string order;
        vector<vector<int>> graph(26);
        vector <bool> completedLetters(26, false);
        vector <bool> dictionary(26);
        for(auto word : words)
            for(auto letter : word)
                dictionary[letter - 'a'] = true;
        BuildGraph(words, graph);
        for(int i = 0; i < graph.size(); i++){
            vector <bool> usedLetters(26, false);
            if(!completedLetters[i] && dictionary[i])
                if(!DeepFirstSearch(i, graph, completedLetters, usedLetters, order))
                  return {};
        }
        return order;
    }
 
};
```
