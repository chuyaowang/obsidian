# Assignment 1


$$
\begin{align}
v&= \frac{V_{max}S_{1}S_{2}}{K_{m_{1}}S_{2}+K_{m_{2}}S_{1}+S_{1}S_{2}} \\
K_{m_{1}}S_{2}+K_{m_{2}}S_{1}+S_{1}S_{2}&=\frac{V_{max}S_{1}S_{2}}{v} \\
K_{m_{2}}S_{1}&=\frac{V_{max}S_{1}S_{2}}{v}-K_{m_{1}}S_{2}-S_{1}S_{2} \\
K_{m_{2}}&=\frac{1}{S_{1}}\left( \frac{V_{max}S_{1}S_{2}}{v}-K_{m_{1}}S_{2}-S_{1}S_{2} \right) \\
K_{m_{2}}&=\frac{V_{max}S_{2}}{v}-\frac{K_{m_{1}}S_{2}}{S_{1}}-S_{2}
\end{align}
$$

$$
\begin{align}
V_{max}&=\frac{V_{max}K_{m_{1}}S_{2}}{K_{m_{1}}S_{2}+K_{m_{2}}K_{m_{1}}+K_{m_{1}}S_{2}} \\
K_{m_{2}}K_{m_{1}}+K_{m_{1}}S_{2}&=0 \\
K_{m_{2}}=-S_{2}
\end{align}
$$

$$
\begin{align}
v&=-K_{m_{1}}\cdot \frac{v}{S_{1}}+V_{max}\\ \\
&=-K_{m_{1}}\cdot \frac{1}{S_{1}}\cdot \frac{V_{max}S_{1}S_{2}}{K_{m_{1}}S_{2}+K_{m_{2}}S_{1}+S_{1}S_{2}} + V_{max}
\end{align}

$$
## Question 2

row: reactant
column: reaction



$$
\begin{bmatrix}
- & \text{v1} & \text{v2} & \text{v3} & \text{v4} & \text{v5} & \text{v6} & \text{v7} & \text{v8} & \text{v9} \\
CIT & 1  & -1 & 0 & 0 & 0 & 0 & 0 & 0 & 0\\
ICIT & 0 & 1 & -1 & 0 & 0 & 0 & 0 & 0 & 0\\
AKG & 0 & 0 & 1 & -1 & 0 & 0 & 0 & 0 & 0\\
SCA & 0 & 0 & 0 & 1 & -1 & 0 & 0 & 0 & 0\\
SUCC & 0 & 0 & 0 & 0 & 1 & -1 & 0 & 0 & 0\\
FUM & 0 & 0 & 0 & 0 & 0 & 1 & -1 & 0 & 0\\
MAL & 0 & 0 & 0 & 0 & 0 & 0 & 1 & -1 & 0\\
OAA & -1 & 0 & 0 & 0 & 0 & 0 & 0 & 1 & -1\\
X & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 1
\end{bmatrix}\cdot
\begin{bmatrix}
\text{v1} \\ \text{v2} \\ \text{v3} \\ \text{v4} \\ \text{v5} \\ \text{v6} \\ \text{v7} \\ \text{v8} \\ \text{v9}
\end{bmatrix}=0
$$


```
ffmpeg -ss 30 -t 3 -i mika.mp4 \
    -vf "fps=10,scale=320:-1:flags=lanczos,split[s0][s1];[s0]palettegen[p];[s1][p]paletteuse" \
    -loop 0 output.gif
```

ffmpeg -t 10 -i mika.mp4 -vf "fps=10,scale=320:-1:flags=lanczos" -y palette.png
ffmpeg -t 10 -i mika.mp4 -i palette.png -filter_complex "fps=10,scale=320:-1:flags=lanczos,paletteuse" output.gif
