In an exam room, there are N seats in a single row, numbered `0, 1, 2, ..., N-1`.

When a student enters the room, they must sit in the seat that maximizes the distance to the closest person.  If there are multiple such seats, they sit in the seat with the lowest number.  (Also, if no one is in the room, then the student sits at seat number 0.)

Return a class `ExamRoom(int N)` that exposes two functions: `ExamRoom.seat()` returning an int representing what seat the student sat in, and `ExamRoom.leave(int p)` representing that the student in seat number p now leaves the room.  It is guaranteed that any calls to `ExamRoom.leave(p)` have a student sitting in seat p.

 

Example 1:

Input: `["ExamRoom","seat","seat","seat","seat","leave","seat"], [[10],[],[],[],[],[4],[]]`

Output: `[null,0,9,4,2,null,5]`

Explanation:

`ExamRoom(10) -> null`

`seat() -> 0, no one is in the room, then the student sits at seat number 0.`

`seat() -> 9, the student sits at the last seat number 9.`

`seat() -> 4, the student sits at the last seat number 4.`

`seat() -> 2, the student sits at the last seat number 2.`

`leave(4) -> null`

`seat() -> 5, the student sits at the last seat number 5.`



```java
class ExamRoom {
    
    TreeSet<int[]> rangeSet;
    TreeSet<Integer> occupiedSeat;
    int N; 

    public ExamRoom(int N) {
        
        this.N = N;
        rangeSet = new TreeSet<>(new Comparator<int[]>() {
            public int compare(int[] a, int[] b) {
                int dist1 = ((a[0] == 0 || a[1] == N - 1) ? a[1] - a[0] : (a[1] - a[0]) / 2);
                int dist2 = ((b[0] == 0 || b[1] == N - 1) ? b[1] - b[0] : (b[1] - b[0]) / 2);
                //distance to the closest element...consider the boundry case...
                int res = dist1 - dist2;
                if (res != 0) return res;
                return b[0] - a[0];
            }
        });
        occupiedSeat = new TreeSet<>();
       
        rangeSet.add(new int[] {0, N - 1});
    }
    
    public int seat() {
        if (rangeSet.size() == 0) return -1;
        int[] seg = rangeSet.last();
        rangeSet.remove(seg);
        if (seg[0] == 0) {
            if (seg[1] >= 1) {
                rangeSet.add(new int[] {1, seg[1]});
            }
            occupiedSeat.add(0);
            return 0;
        } 
        if (seg[1] == N - 1) {
            if (N - 2 >= seg[0]) {
                rangeSet.add(new int[] {seg[0], N - 2});
            }
            occupiedSeat.add(N - 1);
            return N - 1;
        }
        int mid = seg[0] + (seg[1] - seg[0]) / 2;
        if (mid - 1 >= seg[0]) {
            rangeSet.add(new int[] {seg[0], mid - 1});
        }
        if (mid + 1 <= seg[1]) {
            rangeSet.add(new int[] {mid + 1, seg[1]});
        }
        occupiedSeat.add(mid);
        return mid;
    }
    
    public void leave(int p) {
        Integer pre = occupiedSeat.lower(p);
        Integer post = occupiedSeat.higher(p);
        int start = 0, end = N - 1;
        if (pre != null) {
        
            start = pre + 1;
        }
        rangeSet.remove(new int[] {start, p - 1}); //may sit out of the loop
        if (post != null) {
            end = post - 1;
        }
        rangeSet.remove(new int[] {p + 1, end});
        occupiedSeat.remove(p);
        rangeSet.add(new int[] {start, end});
    }
}

/**
 * Your ExamRoom object will be instantiated and called as such:
 * ExamRoom obj = new ExamRoom(N);
 * int param_1 = obj.seat();
 * obj.leave(p);
 */
 ```
