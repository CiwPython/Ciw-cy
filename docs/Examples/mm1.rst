.. _m-m-1:

==================================
Enghraifft - Efelychu System M/M/1
==================================

Fan hyn rhoddir esiampl o system M/M/1, a chymharir canlyniadau'r efelychiad hwn gyda chanlyniadau a rhoddir gan theori ciwio.
Bydd y tudalen hwn yn gweithio trwy enghraifft o system M/M/1 gyda dyfodiadau Poisson cyfradd 3 ac amseroedd gwasanaeth esbonyddol cyfradd 5.

Mae theori ciwio yn rhoi'r amser aros cymedrig yn system M/M/1 fel :math:`\mathbb{E}[W] = \frac{\rho}{\mu(1-\rho)}`. Wrth fewnbynnu cyfradd dyfodiad :math:`\lambda = 3` a chyfradd wasanaeth :math:`\mu = 5`, derbyniwn ddwysedd traffig  :math:`\rho = \frac{\lambda}{\mu} = 0.6`, ac felly :math:`\mathbb{E}[W] = 0.3`.

Sefydlwch y paramedrau o fewn ciw::

    >>> params_dict = {'Arrival_distributions': {'Class 0': [['Exponential', 3.0]]},
    ...                'Service_distributions': {'Class 0': [['Exponential', 5.0]]},
    ...                'Simulation_time': 250,
    ...                'Transition_matrices': {'Class 0': [[0.0]]},
    ...                'Number_of_servers': [1]
    ...                }

Mae'r cod canlynol yn ailadrodd yr arbrawf 100 gwaith, ond yn recordio'r amseroedd aros ar gyfer cwsmeriaid a chyrhaeddwyd wedi'r amser cynhesu 50.
Mae'n dychwelyd amser aros cymedrig y system::
    
    >>> import ciw
    >>> from random import seed
    >>> def iteration(warmup):
    ...     Q = ciw.Simulation(params_dict)
    ...     Q.simulate_until_max_time()
    ...     records = Q.get_all_records(headers=False)
    ...     waits = [row[4] for row in records if row[3] > warmup]
    ...     return sum(waits)/len(waits)
    
    >>> seed(27)
    >>> ws = []
    >>> for i in range(100):
    ...     ws.append(iteration(50))
    
    >>> print sum(ws)/len(ws)
    0.292014274888

Gwelwn fod canlyniadau'r efelychiad yn cytuno gyda chanlyniadau theori ciwio.