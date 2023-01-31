## Threshold setting : 
- if it is positive data, to increase than threshold
- if it is negative data, to decrease than threshold

## Test :
- data를 모든 label에 대해서 layer를 통과시키고, 
- 모든 layer에 대해서 goodness를 더했을 때 가장 높은 goodness를 가지는 label일 때가 정답이다.

## All of data :
- data는 layer에 들어갈때, label에 대한 정보와 같이 들어간다 (본 예제에선 x[:, :10]으로, 앞의 10개의 pixel을 0으로 초기화 시킨후 실제 y label의 index에만 x.max()로 값을 준다)
- ex) True y label : 3, [0 0 0 2.25 0 0 0 0 0 0]


## Update :
- 한 layer에 대해서 input 넣고, update(backward)해도 된다. 어차피 Loss function은 각 layer마다 존재
- 본 예제에선 (positive data, negative data)를 가지고 와서 각 layer마다 차례대로 positive data, negative data를 통과시킨 후 그 평균 값들이 (노드들에 대해서 평균) loss 함수에 의해 backward된다.
- forward시, 각 노드들에 대한 연산은 activation( XW + Bias )이다. 
- backward시, forward의 output을 제곱 후 node에 대해서 평균을 구한다. 
- backward가 끝나면, layer에서 나온 output 값을 다음 layer에게 전달한다 (당연히 다음 layer에게 전달할 때는 .detach()를 해준다). 즉 처음 input에만 x + label이 들어감 

## Create negative data
- 본 예제에서는 기존의 data x에다, y label을 [code] rnd = torch.randperm(x.size(0)) 로 섞어서 줌으로써 negative data를 만들었다.

[참고 github](https://github.com/mohammadpz/pytorch_forward_forward)
