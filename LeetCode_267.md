# palindrome permutation II
Problem Link: [Palindrome Permutation II](https://leetcode.com/problems/palindrome-permutation-ii/)
Level: Medium
Appeared: Uber


## Thoughts
1)Need to check if the string could be rearrange to a palindrome. Reference [Palindrome Permutation](https://leetcode.com/problems/palindrome-permutation/)

Solution: check if there exists two or more characters that appears odd times in the string.

2)Generare unique permutation for the half of the string (preprocess before rebuilding the palindrome). Reference [Permutations II](https://leetcode.com/problems/permutations-ii/)

## Code
### Python:
```
class Solution:
    def generatePalindromes(self, s: str) -> List[str]:
        d=collections.Counter(s)
        cnt=0
        p=''
        for c in d:
            if d[c]%2==1:
                cnt+=1
                p=c
                d[c]-=1
                if cnt==2:
                    return []
        out = [[]]
        for c in d:
            for i in range(d[c]//2):
                out2 = []
                for l in out:
                    for i in range((l+[c]).index(c)+1):
                        out2.append(l[:i]+[c]+l[i:])
                out[:] = out2[:]
        if p:
            for i in range(len(out)):
                out[i]=out[i]+[p]+out[i][::-1]
        else:
            for i in range(len(out)):
                out[i]=out[i]+out[i][::-1]
        return list(map(lambda x:''.join(x),out))
```
No extra time and O(n) extra space.
