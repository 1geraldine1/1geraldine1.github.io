---
title: "MMSkeleton & DeepLabCut 예제 돌려본 후기"
date: 2022-07-07T18:08:30-04:00
categories:
  - '2022-07 TIL'
tags:
  - '20220707'
  - 'TIL'
  - 'MMSkeleton'
  - 'DeepLabCut'
  - 'Pose estimation'
---

# 개요

* 반려동물 행동예측 프로젝트에서, AI Hub 데이터셋에 첨부되어있던 모델중 유니스트에서 개발한 예제 코드는 MMSkeleton과 DeepLabCut 두가지 라이브러리를 핵심 요소로 사용하고 있었다.

* DeepLabCut을 통해 영상에서 각 프레임별 Skeleton을 추출하고, MMSkeleton을 이용해 각 Skeleton을 GCN으로 만들어 Pose estimation을 수행한다.

* 따라서 두 라이브러리 모두 어느정도 이해도가 있어야 할것으로 판단하여, 각 라이브러리에서 제공하는 예제코드를 실행해보기로 했다.

# MMSkeleton 예제

* [실행한 예제](https://github.com/open-mmlab/mmskeleton/blob/master/doc/GETTING_STARTED.md)

* 사실 이 글을 적기 최소 이틀 전부터 MMSkeleton 예제를 돌리려고 계속 시도했다.

* 온갖 종류의 호환성 에러들이 발생했고, 패키지 호환성 맞추는데만 이틀정도 소비했다.

* 삽질끝에 대부분의 에러들은 다 해결했으나, MMSkeleton에서 pose estimation을 수행하기 위한 NMS(Non-Maximum Suppression) 알고리즘에 해당하는 부분의 코드가 linux 기반이 아니라면 도저히 작동하지 않게끔 제작되어있었다.

* Faster-RCNN의 코드 기반이라서 [MrGF님의 py-faster-rcnn-windows](https://github.com/MrGF/py-faster-rcnn-windows)라던지 여러가지 응용해서 시도해봤다.

  * 하지만 Cython을 통해 변환된 cpp파일에서 난 오류가 [해결책(Q9 참조)](https://blog.csdn.net/jiajunlee/article/details/50373815)에도 정상적으로 작동하지 않았다.

* 예제 돌리느라 이것저것 리서치 하는 과정에서 해당 라이브러리의 지원이 중단되었음을 눈치챌수 있었다.

* 본 프로젝트에서는 지원이 중단된 MMSkeleton 대신, [MMPose](https://github.com/open-mmlab/mmpose)를 사용해야겠다고 결심했다.

# DeepLabCut 예제

* [실행한 예제](https://github.com/DeepLabCut/DeepLabCut/blob/master/examples/COLAB/COLAB_3miceDemo.ipynb)

* MMSkeleton이 망해버려서 이것까지 망하면 큰일난다는 심정으로 DeepLabCut의 예제를 찾아 실행해보았다.

* 다행히도 colab을 통해 실행되는 예제가 있었고, 그대로 돌려보니 별 탈 없이 잘 실행되는것을 확인할수 있었다.

* 조금만 수정하면 로컬에서도 별 무리없이 돌릴수 있을것으로 기대되어, 여러모로 내일이 기대된다.




