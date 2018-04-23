---
layout: post
title: 
category: 算法
tags: Algorithm
keywords: BSF
description: deliver message
---

题目描述：给一个公司的人员信息，第i个人传递消息的时间花费为t[i]，下属名单为list[i]。当某人接到消息后他会马上传递给他的所有下属，0号人物是CEO。现在CEO发布了一个消息传递下去，问公司里面所有人都收到消息的时间是多少？
代码：

int deliverMessage(vector<int> t, vector<vector<int>> subordinate) {
    if(t.size() == 0 || t.size() != subordinate.size()) {
        return -1;
    }

    vector<int> visit(t.size(), -1);
    
    int ans = 0;
    queue<int> q;
    q.push(0);
    visit[0] = 0;

    while(!q.empty()) {
        int x = q.back();
        q.pop();

        for(int i=0; i<subordinate[x].size(); ++i) {
            int v = subordinate[x][i];
            if(visit[v] == -1) {
                visit[v] = t[x] + visit[x];
                if(visit[v] > ans) {
                    ans = visit[v];
                }
            }
            q.push(v);
        }
    }
    return ans;
}
