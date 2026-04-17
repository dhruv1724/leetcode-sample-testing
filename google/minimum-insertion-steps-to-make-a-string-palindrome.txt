class Solution {
public:
    int find(string s,int start,int end,vector<vector<int>>&dp){
        if(start==end){
            return 0;
        }
        if(start>end){
            return 0;
        }
        if(dp[start][end]!=-1) return dp[start][end];
        if(s[start]==s[end]){
            //no insertion
            return dp[start][end]=find(s,start+1,end-1,dp);
        }else{
            //ya toh start ki side insert krdo and move the other end
            //or insert at end and move the start
            return dp[start][end]=1 + min(find(s,start+1,end,dp),find(s,start,end-1,dp));
        }
    }
    int findUsingTab(string s){
        int n=s.size();
        vector<vector<int>>dp(s.size(),vector<int>(s.size(),0));
        //i need ans of d[0][n-1]
        // for(int i=0;i<n;i++){
        //     for(int j=0;j<n;j++){
        //         if(i==j){
        //             dp[i][j]=0;
        //         }
        //         if(i>j){
        //             dp[i][j]=0;
        //         }
        //     }
        // }
        for(int start=n-2;start>=0;start--){
            for(int end=1;end<n;end++){
                if(start==end){
                    dp[start][end]=0;
                    continue;
                }
                if(start>end){
                    dp[start][end]=0;
                    continue;
                }
                if(s[start]==s[end]){
                    //no insertion
                    dp[start][end]=dp[start+1][end-1];
                }else{
                    //ya toh start ki side insert krdo and move the other end
                    //or insert at end and move the start
                    dp[start][end]=1 + min(dp[start+1][end],dp[start][end-1]);
                }
            }
        }
        return dp[0][n-1];
    }
    int minInsertions(string s) {
        int start=0;
        int end=s.size()-1;
        // vector<vector<int>>dp(s.size(),vector<int>(s.size(),-1));
        int ops=findUsingTab(s);
        return ops;
    }
};