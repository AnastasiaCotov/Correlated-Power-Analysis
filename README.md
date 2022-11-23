# CPA – correlated power analysis attack CUDA implementation
Correlation Power Analysis (CPA) is an efficient technique for recovering secret key bytes of a cryptographic algorithm implementation by analysing the power traces of its execution. Although CPA usually does not require a lot of traces to recover secret key bytes, it is no longer true in a noisy environment, for which the required number of traces can be very high. Computation time can then become a major concern for performing this attack and assessing the robustness of implementation against it.
The objective is to observe how a GPU-based CPA attack can be sped up compared to a running attack on the CPU.
The project consists of GPU implementation of CPA – correlation power analysis attack having given the collected power trances in a hardware device which was running AES128 encryption algorithm.

# The Strategy
🡺 Build a matrix of Estimated Power Traces using the hamming distance between plaintext and guessed key values

🡺 Calculate the Pearson correlation coefficient between the modelled and actual power consumption. Do this for every data point in the traces

🡺 Analyse the correlation results

🡺 Save the results in 16 CSV files, each of them corresponds to 1 byte of the secret key

# Conclusions
In the end we managed to write a faster version of the correlation power analysis. With normal CPU implementation, one iteration which is the calculation for one possible value of that byte was taking around 16 seconds. Using Numba instead for the correlation calculation was 1.7 seconds. After we parallelized all the loops, we managed to reduce it to 0.8 seconds per iteration.
So, our method achieves up to ×20 speedups compared to the original CPU CPA implementation and is particularly efficient when the number of traces is high.
