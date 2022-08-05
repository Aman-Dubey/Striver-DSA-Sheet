DAY::4

#2-sum-Problem

class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        map<int,int> mp;
        vector<int> ans;
        int n=nums.size();
        for(int i=0;i<n;i++) {
            if(mp.find(nums[i])!=mp.end()) {
                ans.push_back(i);
                ans.push_back(mp[nums[i]]);
                return ans;
            }
            mp[target-nums[i]]=i;
        }
        return ans;
    }
};

#4-sum-Problem

class Solution {
public:
    vector<vector<int>> fourSum(vector<int>& nums, int target) {
        vector<vector<int>> ans;
        int n=nums.size();
        if(n<4) return ans;
        sort(nums.begin(),nums.end());
        for(int i=0;i<n-3;i++) {
            for(int j=i+1;j<n-2;j++) {
                int start=j+1, end=n-1;
                long int tt=target;
                long long int remaining = tt-nums[i]-nums[j];
                while(start<end) {
                    int currSum=nums[start]+nums[end];
                    if(currSum > remaining) end--;
                    else if(currSum < remaining) start++;
                    else{
                        vector<int> temp;
                        temp.push_back(nums[i]);
                        temp.push_back(nums[j]);
                        temp.push_back(nums[start]);
                        temp.push_back(nums[end]);
                        ans.push_back(temp);
                        start++;
                        while(start<end && nums[start]==nums[start-1]) start++;
                        while(start<end && nums[end]==nums[end-1]) end--;
                    }
                }
                while(j<n-2 && nums[j]==nums[j+1]) j++;
            }
            while(i<n-3 && nums[i]==nums[i+1]) i++;
        }
        return ans;
    }
};

#Longest Consecutive Sequence

class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        int n=nums.size();
        if(n==0) return n;
        unordered_map<int,bool> isPresent;
        for(int i=0;i<n;i++) isPresent[nums[i]]=true;
        int ans=1;
        for(int i=0;i<n;i++) {
            if(isPresent.find(nums[i]-1)==isPresent.end()) {
                int tempCount=1,count=nums[i];
                while(isPresent.find(count+1)!=isPresent.end()){
                    tempCount++;
                    count++;
                }
                ans=max(ans,tempCount);
                
            }
        }
        return ans;
    }
};

#Largest Subarray with 0 sum

int LongestSubsetWithZeroSum(vector < int > arr) {
  // Write your code here
    int n=arr.size();
    int ans=0,sum=0;
    unordered_map<int,int> mp;
    for(int i=0;i<n;i++) {
        sum+=arr[i];
        if(sum==0) ans=max(ans,i+1);
        if(mp.find(sum)!=mp.end()) {
            ans=max(ans,i-mp[sum]);
        } else mp[sum]=i;
        
    }
    return ans;
}

#Count number of subarrays with given Xor K

#Longest Substring without repeat

class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int ans=0,start=0,n=s.size();
        unordered_map<char,int> charPosition;
        for(int i=0;i<n;i++) {
            if(charPosition.find(s[i])==charPosition.end()) {
                ans=max(ans,i-start+1);
            } else {
                if(charPosition[s[i]] < start)
                ans=max(ans,i-start+1);
                else ans=max(ans,i-start);
                start=max(start,charPosition[s[i]]+1);
            }
            charPosition[s[i]]=i;
        }
        return ans;
    }
};

