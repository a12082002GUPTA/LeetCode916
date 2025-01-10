# LeetCode916
# C++
class Solution {
public:
    vector<string> wordSubsets(vector<string>& words1, vector<string>& words2) {
        vector<int>v(26,0);
        for(int i=0;i<words2.size();i++)
        {
            vector<int>freq(26,0);
            for(int j=0;j<words2[i].length();j++)
            {
                freq[words2[i][j]-97]++;
                v[words2[i][j]-97]=max(v[words2[i][j]-97],freq[words2[i][j]-97]);
            }
        }
        vector<string>ans;
        for(int i=0;i<words1.size();i++)
        {
            vector<int>v1(26,0);
            for(int j=0;j<words1[i].length();j++)
            {
                v1[words1[i][j]-97]++;
            }
            int f=0;
            for(int j=0;j<26;j++)
            {
                if(v[j]>v1[j])
                {
                    f=1;
                    break;
                }
            }
            if(f==0)
            ans.push_back(words1[i]);
        }
        return ans;
    }
};

# Python

from collections import Counter
from typing import List

class Solution:
    def wordSubsets(self, words1: List[str], words2: List[str]) -> List[str]:
        # Initialize the maximum frequency array for words2
        max_freq = [0] * 26
        
        for word in words2:
            freq = [0] * 26
            for char in word:
                freq[ord(char) - ord('a')] += 1
                max_freq[ord(char) - ord('a')] = max(max_freq[ord(char) - ord('a')], freq[ord(char) - ord('a')])
        
        result = []
        for word in words1:
            freq = [0] * 26
            for char in word:
                freq[ord(char) - ord('a')] += 1
            
            # Check if `word` in `words1` satisfies all conditions
            if all(freq[i] >= max_freq[i] for i in range(26)):
                result.append(word)
        
        return result

# Java

import java.util.*;

class Solution {
    public List<String> wordSubsets(String[] words1, String[] words2) {
        // Create a frequency array to store the maximum frequency of each character in words2
        int[] maxFreq = new int[26];
        
        for (String word : words2) {
            int[] freq = new int[26];
            for (char ch : word.toCharArray()) {
                freq[ch - 'a']++;
                maxFreq[ch - 'a'] = Math.max(maxFreq[ch - 'a'], freq[ch - 'a']);
            }
        }
        
        List<String> result = new ArrayList<>();
        
        for (String word : words1) {
            int[] freq = new int[26];
            for (char ch : word.toCharArray()) {
                freq[ch - 'a']++;
            }
            
            // Check if the current word in words1 satisfies the condition
            boolean isUniversal = true;
            for (int i = 0; i < 26; i++) {
                if (freq[i] < maxFreq[i]) {
                    isUniversal = false;
                    break;
                }
            }
            
            if (isUniversal) {
                result.add(word);
            }
        }
        
        return result;
    }
}
