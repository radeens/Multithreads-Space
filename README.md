##Space Simulation Rules

We will begin by describing how the space simulation works. In the simulation, there will be starships traveling between starports, and passengers traveling between starports, each with an itinerary. There are a number of rules governing how starships and travelers may move between starports.

##Starports
      A list of starports (and its capacity in ships) is provided.
##Starships
    A list of starships (and its capacity in travelers) is provided.
    Starships are initially in space (not docked to a starport).
    Starships visit starports, in order from first to last in the list. When a starship visits the last starport in the list, it repeats the process starting from the first starport on the list.
    The total number of starships docked at a starport must not exceed the capacity of the starport. If there are multiple starships waiting to dock with a starport, the order they dock is unspecified.
##Travelers
    A list of travelers (and their itinerary) is provided.
    Each traveler's itinerary specifies which starport they must visit, and in which order. Travelers ride starships from port to port on their itinerary until they reach their final destination.
    The same starport may occur on the itinerary multiple times, but may not be adjacent to itself.
    At the start of the simulation, each traveler is at the first starport on their itinerary.
    Travelers wait at starports until a starship arrives, then try to board the starship and ride it to the next starport on the traveler's itinerary. Travelers may ride aboard any starship, as long as the capacity of the starship is not exceeded. If multiple travelers are trying to board a starship, the order they do so is unspecified.
    When a starship carrying a traveler arrives at the next starport on the traveler's itinerary, the traveler may attempt to disembark (depart the starship and enters the starport) while the starship is docked to the starport.
    It is possible that a traveler at a starport may miss boarding a starship as it passes through. In that case, the traveler remains at the starport and waits for an opportunity to board another starship.
    Similarly, a traveler riding on a starship may miss the opportunity to leave the starship while it is in port. In that case the traveler remains on the starship to wait for another opportunity to disembark at the desired starport.
    Travelers continue moving from starport to starport until they reach the final starport on their itinerary.
    The simulation ends when all travelers reach the final starport on their itinerary.

##Space Simulation Outputs
    A space simulation may be described by a number of simulation events, and the order they occur. 
    Four simulation events and their associated messages are:
          starship docking at starport
          starship departing from starport
          traveler boarding starship at starport
          traveler departing starship at starport

The simulator must output these simulation messages in the order they occur. These messages (and their order of occurrence) may then be analyzed and used to either display the state of the simulation, or to discover whether the simulation results are valid.
Because the simulation is multithreaded, the order messages are output is dependent on the thread scheduler. Running the same simulation will likely produce different outputs each time.

The simulation output provided in the public tests is simply an example of one possible output. The output of your simulator does not need to match it exactly. In fact it will be unlikely for your simulation output to be identical to the example output provided, especially for large numbers of threads.

##Space Simulation Parameters

Each space simulation is performed for a specific set of simulation parameters. These parameters are stored in a simulation file, and include the following:
      Starports - name of each starport and its capacity
      Starships - name of each starship and its capacity
      Travelers - name of each traveler followed by list of starports in itinerary
Output - possible simulation output for simulation
##The following is an example simulation file:
      === Starports ===
      Earth 1
      Vulcan 1
      === Starships ===
      Enterprise 1
      === Travelers ===
      Kirk Earth Vulcan 
      === Output ===
      Enterprise docking at Earth
        Kirk boarding Enterprise at Earth
      Enterprise departing from Earth
      Enterprise docking at Vulcan
        Kirk departing Enterprise at Vulcan

##Space Simulation Driver

Code is provided in the initial space.rb file to read in (and print out) the simulation parameters. Code is also provided to examine the command line parameters specifying the file containing simulation parameters, and whether the program should perform a simulation or simply display or verify the feasibility of the simulation output. 
##The program may be invoked as:
     ruby space.rb [simulate|display|verify] simFileName
So typing ruby space.rb simulate public1.in would execute a simulation using the simulation parameters in public1.in (ignoring any example simulation output in the file), while typing ruby space.rb verify public1.in would perform an analysis of the simulation output in public1.in to determine whether it is feasible.
The code in space.rb outputs simulation parameters before simulation output, so that its output (if saved in a file) may be passed directly to the simulation display/verify routines for use in debugging your simulation.
