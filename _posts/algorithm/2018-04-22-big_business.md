---
layout: post
title: Big business
category: 算法
tags: Algorithm
keywords: Greedy
description: big business
---

题目描述：给出两个数组a，b。a[i]代表第i部影片的版权费，b[i]代表第i部影片能卖的钱，现在本金k，问最后最多能赚多少钱。(每部影片只需要买一次版权，只能卖一次)
代码:

#include<vector>
#include<map>
#include<iostream>
using namespace std;

int bigBusiness(vector<int> a, vector<int> b, int k) {
    int maxProfit = 0;
    if(a.size() == 0 || a.size() != b.size() || k <= 0) {
        return maxProfit;
    }

    multimap<int, int> profitMmap;

    for(int i=0; i<a.size(); i++) {
        int profit = b[i] - a[i];
        if(profit > 0) {
            profitMmap.insert(pair<int, int>(profit, a[i]));
        }
    }

    for(multimap<int, int>::reverse_iterator it = profitMmap.rbegin(); it != profitMmap.rend(); ++it) {
        if(k >= it->second) {
            k -= it->second;
            maxProfit += it->first;
        } else {
            if(k == 0) {
                break;
            }
        }
    }
    return maxProfit;
}

int main() {
    vector<int> a;
    a.push_back(1);
    a.push_back(2);
    a.push_back(100);
    a.push_back(0);
    a.push_back(-1);

    vector<int> b;
    b.push_back(100);
    b.push_back(200);
    b.push_back(500);
    b.push_back(300);
    b.push_back(-2);

    int k = 100;
    
    // a = [1, 2, 100, 0, -1];
    // b = [100, 200, 500, 300, -2];
    // k = 100;
    
    int maxProfit = bigBusiness(a, b, k);
    cout<<"maxProfit: " << maxProfit << endl;
    return 0;
}
