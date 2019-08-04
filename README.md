import java.util.Scanner;
class Vasya{

	private static void buildtree(int A[], int B[], int tree[], int index, int start, int end){

		if(start == end){
			tree[index] = start;
			return ;
		}
		int mid = (start + end)/2;
		buildtree(A, B, tree, 2*index, start, mid);
		buildtree(A, B, tree, 2*index +1, mid+1, end);
		if(A[tree[2*index]] > A[tree[2*index+1]])
			tree[index] = tree[2*index];
		else if(A[tree[2*index]] == A[tree[2*index+1]])
		{
			if(B[tree[2*index]]<=B[tree[2*index+1]])
				tree[index] = tree[2*index];
			else
				tree[index] = tree[2*index+1];
		}
		else
			tree[index] = tree[2*index+1];

	}
	private static int ans(int A[], int B[], int tree[],int index, int start, int end, int l, int r){
		if(l>end || r<start)
                return -1;
        if(l<=start && r>=end) 
        	return tree[index];
        int mid = (start + end)/2;
        int ans1 = ans(A, B, tree, 2*index, start, mid, l, r);
        int ans2 = ans(A, B, tree, 2*index+1, mid+1, end, l, r);
        if(ans1 != -1 && ans2 != -1){
        	if(A[ans1] > A[ans2])
        		return ans1;
        	else if(A[ans1] == A[ans2]){
        		if(B[ans1] <= B[ans2])
        			return ans1;
        		else
        			return ans2;
        	}
        	else
        		return ans2;
        }
        else if(ans1 != -1)
        	return ans1;
        return ans2;

	}

	public static void main(String [] args){
		Scanner input = new Scanner(System.in);
		int n = input.nextInt();
		int A[] = new int[n];
		int B[] = new int[n];
		for(int i = 0; i < n ;i++)
			A[i] = input.nextInt();
		for(int i = 0; i < n; i++)
			B[i] = input.nextInt();
		int tree[] = new int[4*n];
		buildtree(A, B, tree, 1, 0, n-1);
		int Q = input.nextInt();
		while(Q-- > 0){

			int l = input.nextInt()-1;
			int r = input.nextInt()-1;
			int ans = ans(A, B, tree, 1, 0, n-1, l, r);
			System.out.println(ans + 1);
		}
	}
}
