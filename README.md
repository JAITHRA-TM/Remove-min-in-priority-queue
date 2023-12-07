# Remove-min-in-priority-queue
#include <vector>

class PriorityQueue {
    vector<int> pq;

   public:
    bool isEmpty() { 
        return pq.size() == 0; 
    }

    int getSize() { 
        return pq.size(); 
    }

    int getMin() {
        if (isEmpty()) {
            return 0;
        }

        return pq[0];
    }

    void insert(int element) {
        pq.push_back(element);

        int childIndex = pq.size() - 1;

        while (childIndex > 0) {
            int parentIndex = (childIndex - 1) / 2;

            if (pq[childIndex] < pq[parentIndex]) {
                int temp = pq[childIndex];
                pq[childIndex] = pq[parentIndex];
                pq[parentIndex] = temp;
            } else {
                break;
            }

            childIndex = parentIndex;
        }
    }

    int removeMin() {
        // Write your code here
        if(isEmpty()){
            return 0;
        }
        int n = pq.size()-1;
        int ans = pq[0];
        pq[0] = pq[n];
        pq.pop_back();
        int pI = 0;
        int lci = (2*pI) + 1;
        int rci = (2*pI) + 2;
        while(lci < pq.size()){
            int mI = pI;
            if(pq[mI] > pq[lci]){
                mI = lci;
            }
            if(rci < pq.size() && pq[mI] > pq[rci]){
                mI = rci;
            }
            if(mI == pI){
                break;
            }
            int temp = pq[mI];
            pq[mI] = pq[pI];
            pq[pI] = temp;
            pI = mI;
        lci = (2 * pI) + 1;
        rci = 2 * pI + 2;
        }
        
        return ans;
    }
};
