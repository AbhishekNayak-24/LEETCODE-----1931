# LEETCODE-----1931
PAINTING A GRID WITH THREE DIFFERENT COLORS
//CODE IN JAVA\
class Solution {
    private int m;
    private final int MOD = 1000000007;

    public int colorTheGrid(int m, int n) {
        this.m = m;
        int totalCombinations = (int) Math.pow(3, m);
        int[] dp = new int[totalCombinations];

        for (int i = 0; i < totalCombinations; i++) {
            if (isValid(i)) {
                dp[i] = 1;
            }
        }

        for (int k = 1; k < n; k++) {
            int[] newDp = new int[totalCombinations];
            for (int i = 0; i < totalCombinations; i++) {
                if (dp[i] > 0) {
                    for (int j = 0; j < totalCombinations; j++) {
                        if (isValid(j) && areCompatible(i, j)) {
                            newDp[j] = (newDp[j] + dp[i]) % MOD;
                        }
                    }
                }
            }
            dp = newDp;
        }

        int result = 0;
        for (int count : dp) {
            result = (result + count) % MOD;
        }
        return result;
    }

    private boolean isValid(int combination) {
        int[] colors = new int[m];
        int temp = combination;
        for (int i = 0; i < m; i++) {
            colors[i] = temp % 3;
            temp /= 3;
        }
        for (int i = 1; i < m; i++) {
            if (colors[i] == colors[i - 1]) {
                return false;
            }
        }
        return true;
    }

    private boolean areCompatible(int comb1, int comb2) {
        int[] colors1 = new int[m];
        int[] colors2 = new int[m];
        int temp1 = comb1;
        int temp2 = comb2;
        for (int i = 0; i < m; i++) {
            colors1[i] = temp1 % 3;
            colors2[i] = temp2 % 3;
            temp1 /= 3;
            temp2 /= 3;
        }
        for (int i = 0; i < m; i++) {
            if (colors1[i] == colors2[i]) {
                return false;
            }
        }
        return true;
    }
}
