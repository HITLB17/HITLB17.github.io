---
title: '集群系统建模综述'
date: 2019-12-07
permalink: /posts/2019/12/Intelligent_control_model/
tags:
  - Intelligent control
  - model
---

集群系统模型一般包含两部分：拓扑模型和节点动力学模型。拓扑模型决定了智能体间的连接关系，通常用图表示，如：无向图、有向图、加权图等。节点动力学模型用于描述每个智能体自身的运动规则，通常采用一阶、二阶积分器模型、一般系统模型等方法。

最早的集群系统模型是由Reynolds[1]于1987年提出的Boids模型，该模型用计算机来模拟群体行为，并给出了智能集群系统满足的三个规则：

1）速度匹配：agent尽量与邻居agents速度和方向的平均值保持一致；

2）聚集：agent尽量向邻居agents的平均位置运动；

3）避免碰撞：相邻agents之间避免发生碰撞。

2001年，Reynolds将Boids模型所有资料公布于网站上，包括程序、示例、相关论文等。在Boids模型的基础上，1995年Vicsek等人[2]将其简化，提出了一种离散多智能体模型----Vicsek模型用于模拟大量粒子涌现出一致性的现象，其实质是Boids模型中速度匹配的动力学实现。Vicsek模型刻画了多个粒子构成的自治系统的同步运动．在这个模型中粒子遵循如下规则：

1）系统中运动的粒子具有常速率  ；

2）粒子存在一个影响半径  ，即系统中的任意一对粒子，只有这对粒子之间的直线距离小于  时，他们才存在相互的影响；

3）粒子每一时刻的运动方向跟上一时刻它的影响半径范围内的其他所有粒子的平均运动方向相同。

同时Vicsek模型引入了数学化描述，如公式所示：

$${\rm{x}_i}(t + 1) = {\rm{x}_i}(t) + {\rm{v}_i}(t) \Delta t \\ {\theta _i}(t + 1) = \langle{\theta _i}(t){\rangle_r} + {\Delta _i}(t)$$

其中:  ${\rm{x}_i}(t)$ 为 agent i在t时刻的位置，${v_i}(t)$ 为agent i在t时刻的速度，${\theta _i}(t)$为agent i在t时刻的航向，$<{\theta _i}(t){ > _r}$ 为agent i及其周围agents的航向的平均，${\Delta _i}(t)$为扰动项。利用$\varphi$评判是否同步的标注，如公式：

$$\varphi = \dfrac{1}{N{v_0}} \left| {\sum \limits_{i = 1}^N {\rm{v}}_i} \right|$$

  $\varphi$ 可以描述为归一化的平均速度，当速度一致时， $\varphi =1$ 。完全杂乱无章时，$\varphi=0$ 。
  
  2003年，Jadbabaie等人[3]在无噪声的假设条件下对Vicsek模型进行了简化，用矩阵论和图论（无向图）给出了Vicsek模型的收敛性的理论证明，指出：只要满足联通，粒子的运动方向就能达到一致。与Vicsek描述类似，Jadbabaie引入了图论，将无领导的模型描述为：
 
 $${\theta _i}(t + 1) = \dfrac{1}{1 + k_i (t)} (\theta_i (t) + \sum_{j\in{N_i(t)}}{\theta _j (t)} )$$
 
 其中${k_i}(t)$为agent i周围的agents数目，$\sum_{j\in{N_i(t)}}{\theta _j (t)}$描述为周围agents航向之和，${N_i}(t)$表示t时刻agent i的拓扑连接矩阵。如果agents间距离较远，系统容易发生聚堆、簇分离的情况，因此Jadbabaie等人又引入了虚拟领航员，作为导航项  ，将公式(3)进行修改，得到如公式(4)的系统模型：
 
$${\theta _i}(t + 1) = \dfrac{1}{1 + k_i (t) + b_i (t)} (\theta_i (t) + \sum_{j\in{N_i(t)}}{\theta _j (t)} + b_i (t)\theta _0)$$
 
 当需要领航员的情况下，${b_i}(t)=1$，否则${b_i}(t)=0$。集群系统模型自此从群体动力学模型时代进入了网络化系统与图论描述时代。
  
参考文献

[1]   R. C.W, “Flocks, Herds, and Schools: A Distributed Behavioral Model,” Tech. Coloproctol., vol. 21, no. 2, pp. 25–34, 1987.

[2]   T. Vicsek, A. Czirk, E. Ben-Jacob, I. Cohen, and O. Shochet, “Novel type of phase transition in a system of self-driven particles,” Phys. Rev. Lett., vol. 75, no. 6, pp. 1226–1229, 1995.

[3]   A. Jadbabaie, J. Lin, and A. S. Morse, “Coordination of Groups of Mobile Autonomous Agents Using Nearest Neighbor Rules,” IEEE Trans. Automat. Contr., vol. 48, no. 6, pp. 988–1001, 2003.

[4]   R. Olfati-Saber, J. A. Fax, and R. M. Murray, “Consensus and Cooperation in Networked Multi-AgentSystems,” Proc. IEEE, vol. 95, no. 1, pp. 215–233, 2007.

[5]   R. Olfati-Saber, “Flocking for multi-agent dynamic systems: Algorithms and theory,” IEEE Trans. Automat. Contr., vol. 51, no. 3, pp. 401–420, 2006.

[6]   L. Moreau, “Stability ofMultiagent SystemsWith Time-Dependent Communication Links,” IEEE Trans. Automat. Contr., vol. 50, no. 2, pp. 169–182, 2005.

[7]   R. Olfati-Saber and R. M. Murray, “Consensus problems in networks of agents with switching topology and time-delays,” IEEE Trans. Automat. Contr., vol. 49, no. 9, pp. 1520–1533, 2004.

[8]   W. Ren and R. W. Beard, “Consensus seeking in multiagent systems under dynamically changing interaction topologies,” IEEE Trans. Automat. Contr., vol. 50, no. 5, pp. 655–661, 2005.

[9]   H. Zhang and F. L. Lewis, “Adaptive cooperative tracking control of higher-order nonlinear systems with unknown dynamics,” Automatica, vol. 48, no. 7, pp. 1432–1439, 2012.

[10]  S. Motsch and E. Tadmor, “A New Model for Self-organized Dynamics and Its Flocking Behavior,” J. Stat. Phys., vol. 144, no. 5, pp. 923–947, 2011.

[11]  J. Shen, “Cucker-smale flocking under hierarchical leadership,” SIAM J. Appl. Math., vol. 68, no. 3, pp. 694–719, 2007.

[12]  Z. LI and XIAOPING XUE, “CUCKER–SMALE FLOCKING UNDER ROOTED LEADERSHIP WITH FIXED AND SWITCHING TOPOLOGIES,” SIAM J. Appl. Math., vol. 70, no. 8, pp. 3156–3174, 2010.

[13]  Jiu-Gang Dong, “Flocking under hierarchical leadership with a free-will leader,” Int. J. Robust Nonlinear Control, vol. 18, no. October 2014, pp. 557–569, 2012.

[14]  R. Sepulchre, D. A. Paley, and N. E. Leonard, “Stabilization of planar collective motion: All-to-all communication,” IEEE Trans. Automat. Contr., vol. 52, no. 5, pp. 811–824, 2007.

[15]  A. Papachristodoulou and A. Jadbabaie, “Synchronization in oscillator networks: Switching topologies and non-homogeneous delays,” Proc. 44th IEEE Conf. Decis. Control. Eur. Control Conf. CDC-ECC ’05, vol. 2005, pp. 5692–5697, 2005.

[16]  A. Jadbabaie, N. Motee, and M. Barahona, “On the stability of the Kuramoto model of coupled nonlinear oscillators,” Proc. Am. Control Conf., vol. 5, pp. 4296–4301, 2004.

[17]  W. Gao, Z. P. Jiang, F. L. Lewis, and Y. Wang, “Leader-to-Formation Stability of Multiagent Systems: An Adaptive Optimal Control Approach,” IEEE Trans. Automat. Contr., vol. 63, no. 10, pp. 3581–3587, 2018.

[18]  Y. Wang and Y. Song, “Leader-following control of high-order multi-agent systems under directed graphs: Pre-specified finite time approach,” Automatica, vol. 87, pp. 113–120, 2018.

[19]  Y. Zheng, Y. Zhu, and L. Wang, “Consensus of heterogeneous multi-agent systems,” IET Control Theory Appl., vol. 5, no. 16, pp. 1881–1888, 2011.

[20]  J. M. Kim, J. B. Park, and Y. H. Choi, “Leaderless and leader-following consensus for heterogeneous multi-agent systems with random link failures,” IET Control Theory Appl., vol. 8, no. 1, pp. 51–60, 2014.

[21]  D. Yang, W. Ren, X. Liu, and W. Chen, “Decentralized event-triggered consensus for linear multi-agent systems under general directed graphs,” Automatica, vol. 69, pp. 242–249, 2016.

[22]  C. Nowzari, E. Garcia, and J. Cortés, “Event-triggered communication and control of networked systems for multi-agent consensus,” Automatica, vol. 105, pp. 1–27, 2019.

[23]  Frans A. Oliehoek & Christopher Amato, A Concise Introduction to Decentralized POMDPs. 2015.

[24]  J. Hu and M. P. Wellman, “Nash Q-learning for general-sum stochastic games,” J. Mach. Learn. Res., vol. 4, no. 6, pp. 1039–1069, 2004.

[25]  K. Zhang, Z. Yang, H. Liu, T. Zhang, and T. Başar, “Fully Decentralized Multi-Agent Reinforcement Learning with Networked Agents,” pp. 1–45, 2018.

 
---

[1] http://www.red3d.com/cwr/boids/