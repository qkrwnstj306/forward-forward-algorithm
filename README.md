#Threshold setting : 
- if it is positive data, to increase than threshold
- if it is negative data, to decrease than threshold

#Test :
- data를 모든 label에 대해서 layer를 통과시키고, 
- 모든 layer에 대해서 goodness를 더했을 때 가장 높은 goodness를 가지는 label일 때가 정답이다.

#All of data :
- data는 layer에 들어갈때, label에 대한 정보와 같이 들어간다
- 본 예제에선 (positive data, negative data)를 가지고 와서 각 layer마다 차례대로 positive data, negative data를 통과시킨 후 그 평균 값들이 (노드들에 대해서 평균) loss 함수에 의해 backward된다.
- backward가 끝나면, layer에서 나온 output 값을 다음 layer에게 전달한다. 즉 처음 input에만 x + label이 들어감 

#Update :
- 한 layer에 대해서 input 넣고, update(backward)해도 된다. 어차피 Loss function은 각 layer마다 존재