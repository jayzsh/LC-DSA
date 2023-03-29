## A-1

```cpp
class Solution {
public:
    bool x_contains_y(string s, char character) {

        for (int i = 0; i < s.length(); i++)
            if (s[i] == character)
                return true;

        return false;
    }

    string filterBadParen(string &s) {
        
        string newStr = "";
        vector<char> stack;

        for (int i = 0; i < s.length(); i++)
        {
            switch(s[i])
            {
                case '(':
                    if (
                        (i == s.length() - 1) || 
                        !x_contains_y(s.substr(i + 1, s.length() - i), ')')
                    ) continue;
                    stack.push_back(s[i]);
                    newStr += s[i];
                    break;
                
                case ')':
                    if (stack.size() == 0) continue;
                    stack.pop_back();
                    newStr += s[i];
                    break;

                default:
                    newStr += s[i];
            }
        }
        
        return newStr;
    }

    vector<string> removeInvalidParentheses(string s) {

        string l2r = filterBadParen(s);
        
        string t_str = "";
        for (int i = s.length() - 1; i >= 0; i--)
        {
            if (s[i] == ')')
                t_str += '(';
            else if (s[i] == '(')
                t_str += ')';
            else
                t_str += s[i];
        }
        
        string r2l = filterBadParen(t_str);
        
        vector<string> ret;
        ret.push_back(r2l);
        ret.push_back(l2r);
        
        return ret;
    }
};
```
