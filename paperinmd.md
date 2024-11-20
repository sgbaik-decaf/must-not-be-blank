\documentclass[11pt, letterpaper]{article}
\usepackage{authblk}
\usepackage{amsmath}
\usepackage{caption}
\usepackage{graphicx}

%%%

\title{Geospatial Analytic Framework for Modelling Energy Savings of Truck-Drone Hybrid Deliveries in Arbitrary Cities}
\date{November 2024}

\author[1]{Seung Gyu Baik}
\author[1, 2]{Peter Zhang}
\author[3]{Steven Willits}
\author[3]{Sebastian Scherer}
\affil[1]{Heinz College of Information Systems and Public Policy}
\affil[2]{Department of Civil and Environmental Engineering}
\affil[3]{The Robotics Institute}

%%%

\begin{document}
	\maketitle
	\begin{abstract}
		This is an abstract.
	\end{abstract}
	
	\section{Introduction}
	\subsection{Drones for Last-mile Logistics}
	
	Small, rotary-wing, autonomous aerial vehicles (AAVs), commonly known as \textit{drones}, are anticipated to be an innovative mode of last-mile logistics in the near future. Large-cap businesses including Amazon, Walmart, and Alphabet are exploring commercial applications while some already integrated drones to their delivery operations. Drone delivery has also been depicted in many media productions. In operations research, modelling parcel delivery with drones has been an active area of exploration for many years.
	
	Drone flights are not affected by traffic congestion, road network connectivity, and many other features of the ground, thus making itself an efficient mode of delivery. However, drones have internal limitations from its small size and power systems such as battery capacity and takeoff weight. Most commercial drones have a short radius of action if the drone is carrying a cargo. Even the larger commercial model specialized in cargo delivery, the DJI FlyCart 30, can execute a sortie only 8-14km away with a 1.98kWh battery, when assuming the cargo weighs 40kg. In scenarios with such short radius of action, drones are understood not to be competitive enough against traditional ground vehicle for deliveries.
	
	One interesting idea to compensate this problem is \textit{truck-drone cooperation}. Two different modes of logistics can operate with synchronization and share their corresponding strengths and weaknesses to build an efficient operational model.
	
	\begin{figure*}
	\centering
	\includegraphics[width=0.7\linewidth]{DALLE}
	\caption{A concept image of truck-drone cooperation generated by Dall-E}
	\label{fig:dalle}
	\end{figure*}
	
	\subsection{Operations Research in Truck-Drone Hybrid Vehicle Routing Problem}
	
	The mathematical problem formulation of synchronized truck-drone cooperation for last-mile delivery is first discussed by Murray and Chu (2015) as a name of 'drone-assisted parcel delivery' via a mixed-integer linear programming (MILP) problem. They proposed a novel variant of the classic Travelling Salesman Problem (TSP) called the \textit{Flying Sidekick Travelling Salesman Problem} (FSTSP). Another founding paper by Agatz et al. (2018) proposed \textit{Travelling Salesman Problem with Drones} (TSP-D). They discuss a similar heuristic with a different approach and improved accuracy. Neil et al. (2015) and Wang et al. (2017) also contributed to operations research in synchronized truck-drone cooperation topic. The FSTSP and TSP-D heuristic can optimize the total time of package delivery to a given set of customers by allocating either traditional trucks or drones. Also, drones are launched from and retrieved by the truck, extending the overall range of action. Many heuristics, algorithms, and operational models have been published since the inception of FSTSP and TSP-D, either adding more realistic assumptions and constraints, or improving its robustness and computational efficiency. 
	
	According to a classification framework proposed by Moshref-Javadi and Winkenbach (2021), existing drone logistic models can be categorized into 4 bins: Pure-play Drone-based (PD) models, Unsynchronized Multi-modal (UM) models, Synchronized Multi-modal (SM) models, and Resupply Multi-modal (RM) models. Truck-drone cooperation we discuss in this paper is Synchronized Multi-modal (SM) model, where trucks act as a mobile hub for drones yet trucks themselves can still deliver parcels to locations where drones cannot, or where dispatching a drone is not advantageous.
	
	Relating to the SM bin, a subset of heuristics aims to optimally solve the truck-drone hybrid vehicle routing problem of multiple drones equipped on a single truck. Murray and Raj (2020) propose a heuristic approach called the \textit{multiple Flying Sidekick Travelling Salesman Problem} (mFSTSP) and analysis for a multi-drone single-truck system. They predicted that increasing the number of drones can reduce time with diminishing returns. Poikonen and Golden (2020) propose a \textit{k-Multi-visit Drone Routing Problem} (k-MVDRP) that assumes drones can carry multiple heterogeneous packages. Salama and Srinivas (2022) contribute in expanding the operational model to multiple drones with flexible launch-and-recovery points via simulated annealing and variable neighborhood search algorithm. They propose a formulation called \textit{collaborative truck–drone routing and scheduling problem with flexible launch and recovery locations} (CTDRSP-FL). Thomas et al. (2024) introduces a similar optimizing approach for multiple drones with an option for the drones to be launched and retrieved in between customer locations.
	
	\subsection{Energy and the Environment}
	
	According to the U.S. Environmental Protection Agency (2024), greenhouse gas emissions from the transportation sector was responsible for 28\% of all U.S. anthropogenic greenhouse gas emissions in the year 2022, being the largest contributor. 80\% of sectoral emissions come from light-duty vehicles and medium or heavy-duty trucks. Since the majority of commercial small quadcopter drones are powered by Li-ion batteries without an internal combustion engine, truck-drone cooperation for last-mile delivery potentially can expedite the electrification of the transportation sector and reduce greenhouse gas emissions.
	
	Nonetheless, existing literature shows mixed results on its effectiveness. An empirical energy use model and predictions by Stolaroff et al. (2018) stated that small quadcopter drones will have lower lifecycle emissions per package than carbon-fuel trucks or vans. However, newly built warehouses for these drone operations can consume more energy than saved. A scenario-based analysis by Raghunatha et al (2023) highlighted the limited competency of drones in short range missions. Drones are environmentally efficient (-36\% emission) in long range intercity deliveries than diesel trucks, but worse (+59\% emission) in short range intracity deliveries. Electric trucks, the biggest competitor to delivery drones, greatly outperform drones by cutting emissions by -75\% at least and -92\% at most.
	
	On the other hand, empirical research on energy savings and greenhouse gas emission by Rodrigues et al. (2022), small quadcopter drones carrying a small (0.5kg) package are environmentally efficient. Authors found that drone delivery in urban centers can reduce -94\% of energy use and -84\% greenhouse gas emissions compared to diesel trucks. Also, drones were capable to reduce -31\% of energy use and -29\% greenhouse gas emissions even compared to electric vans. The paper also emphasized that the local energy grid where the system operate in is imperative regarding greenhouse gas emissions.
	
	Also, we found that analyses on the energy use of drone delivery systems are either derived from sight-irrelevant tests in controlled environments or site-specific tests in a specific region. We suspect that not addressing the physical diversity might be the reason of inconsistency across existing literature. Where the drone operate must be incorporated in the computing of energy consumption.
	
	\subsection{Contribution of this Paper}
	
	Joining existing literature from operations research, robotics, and the environmental science domain, we found that the majority of contributions in truck-drone hybrid vehicle routing problem only consider a handful of cities as sample instances if considered at all.	To the best of the authors' knowledge, there is no streamlined process of applying the algorithm to a real-world city. This is worthy of careful consideration because the physical structure of the city, especially road network, governs (1) the location of customers and (2) the connections between customers. Optimizing movement of ground vehicles is most dependent to the shape of the road network where the delivery fleet operates in. If one is to deploy drones to compliment ground vehicles, the effectiveness of the intervention compared to baseline will vary from city to city.
			
	By building a geospatial analytic framework regarding last-mile deliveries with truck-drone cooperation, the main contribution of this paper is bridging the gap between real-world cities and algorithms on paper. The framework developed with this paper will capture the physical diversity of an arbitrary city structure and feed it into an existing heuristic algorithm. By simulating multiple instances of delivery tours, practical insights of implementing a truck-drone hybrid system can be obtained beforehand in any city. Also, the underlying heuristic algorithm is realistic thanks to multiple features from the mFSTSP heuristic solver such as time-minimizing optimization, drone queuing, and drone service time.
	
	As this paper is accompanied with a fully functioning Python package built with existing open source artifacts, it provides a highly adaptable analytic framework ready to be used by both business and policy analysts anywhere.
	
	\section{The Framework}
	
	\begin{figure}
	\centering
	\includegraphics[width=0.9\linewidth]{fig1}
	\caption{Overview of the proposed framework}
	\label{fig:overview}
	\end{figure}
	

	
	
	\subsection{Overview}
	
	An overview of the proposed framework is visualized in Figure \ref{fig:overview}. Once a user defines a city where truck-drone cooperation delivery is to be made and an address for the supply depot, the geospatial simulator will populate hypothetical customer addresses within the city. After approximations of ground travel time and euclidean distance between all customers and the depot are made (travel matrix), this information will be fed into a VRP solver. The VRP solver will compute a near-optimal routing and scheduling plan given the locations of customers and the depot. Once there is a hypothetical plan of when and where the truck and drones should visit, we can predict its energy use. Comparing to results from a classic ground-only VRP, we obtain the difference in predicted energy use, which is energy savings. A Monte Carlo simulation or multiple different customer locations is conducted to address sampling bias.
	
	\subsection{Operations Model and Assumptions}
	

	
	\begin{tabular}{|c|c|}
	\hline
	Takeoff Speed & 5 \\
	\hline
	Landing Speed & 4 \\
	\hline
	Cruise Speed & 12 \\
	\hline
	Yaw (Turn) Speed & Infinite \\
	\hline
	Cruise Altitude &  100m (328ft) AGL \\
	\hline
	Max Parcel Weight & 0.5kg (1.1lbs) \\
	\hline
	Pre-takeoff Prep. & 60s \\
	\hline
	Post-landing Prep. & 120s \\
	\hline
	Customer Service & 60s \\
	\hline
	Battery Capacity & 99.9kWh (359,640J) \\
	\hline
	\end{tabular}
	\captionof{table}{Assumed specifications of drones}
	
	
	
	We leverage the mFSTSP heuristic and its assumptions by Murray and Raj (2020) and adapt as our truck-drone cooperation model. We assume the delivery fleet comprises one ground vehicle and multiple autonomous aerial vehicles (AAVs). The specification of our AAVs are small quadcopter drones that is comparable to DJI M100, weighing 2kg (4.4lbs) and capable to carry a parcel up to 0.5kg (1.1lbs).
	
	
	\subsection{Geospatial Simulator}
	\subsection{Heuristic VRP Solver}
	\subsection{Energy Use Calculator}
	
	\section{A Sample Analysis for Pittsburgh}
	
	\section{Conclusion}
	
	\section{Appendix: Source Code}
	
	
\end{document}