class Solution {
public:
    int lcs(string &str1,string &str2,int i,int j){
        if(i==str1.size() || j==str2.size()){
            return 0;
        }
        if(str1[i]==str2[j]){
            return 1+lcs(str1,str2,i+1,j+1);
        }else{
            return max(lcs(str1,str2,i,j+1),lcs(str1,str2,i+1,j));
        }
    }

    int lcsUsingTab(string &str1,string &str2,vector<vector<int>>&dp){
        //BASE CASE SIZE SE BAHAR VAALE 0
        int n1=str1.size();
        int n2=str2.size();
        for(int i=n1-1;i>=0;i--){
            for(int j=n2-1;j>=0;j--){
                if(str1[i]==str2[j]){
                    dp[i][j]=1+dp[i+1][j+1];
                }else{
                    dp[i][j]=max(dp[i][j+1],dp[i+1][j]);
                }
            }
        }
        return dp[0][0];
    }
    string shortestCommonSupersequence(string str1, string str2) {
        int i=0;
        int j=0;
        vector<vector<int>>dp(str1.size()+1,vector<int>(str2.size()+1,0));
        int len=lcsUsingTab(str1,str2,dp);
        string ans;
        //dp is ready build the ans from 0,0 to last
        while(i<str1.size() && j<str2.size()){
            if(str1[i]==str2[j]){
                ans+=str1[i];
                i++;
                j++;
            }else{
                if(dp[i+1][j]>dp[i][j+1]){
                    //move towards i+1 side but insert the ith element of str1
                    ans+=str1[i];
                    i++;
                }else{
                    ans+=str2[j];
                    j++;
                }
            }
        }
        while(i<str1.size()){
            ans+=str1[i];
            i++;
        }
        while(j<str2.size()){
            ans+=str2[j];
            j++;
        }
        // reverse(ans.begin(),ans.end());
        return ans;
    }
};