.. _custom-distributions:

======================================
Custom Discrete PDFs for Service Times
======================================

ASQ allows users to define their own discrete service time distributions.
An example distribution may look like this:

	+------+------+------+------+------+------+------+
	| P(X) |  0.1 |  0.1 |  0.3 |  0.2 |  0.2 |  0.1 |
	+------+------+------+------+------+------+------+
	|   X  |  9.5 | 10.2 | 10.6 | 10.9 | 11.7 | 12.1 | 
	+------+------+------+------+------+------+------+

In order to define this probability density function, it must be given a name.
Let's call it :code:`my_special_distribution_01`.

In the :code:`parameters.yml` file, under :code:`Serivce_rates`, for the given class and node enter :code:`Custom` and the name of the distribution below it.
An example is shown::

    Service_rates:
      Class 0:
      - - Custom
        - my_special_distribution_01
      - - Exponential
        - 0.1
      Class 1:
      - - Exponential
        - 0.3
      - - Exponential
        - 0.1

This tells ASQ that at Node 1 all Class 0 customers will have their service time drawn from the custom distribution :code:`my_special_distribution_01`.
This distribution hasn;t been defined yet.
To define the distribution, add the following lines to the end of the :code:`parameters.yml` file::

    my_special_distribution_01:
      - - 0.1
        - 9.5
      - - 0.1
        - 10.2
      - - 0.3
        - 10.6
      - - 0.2
        - 10.9
      - - 0.2
        - 11.7
      - - 0.1
        - 12.1

Here we are saying that the value 9.5 will be sampled with probability 0.1, the value 10.2 will be samples with probability 0.1, etc.
This fully defines the custom discrete PDF.

Note:

- For each distribution, probabilities must sum to 1.
- You may add as many custom probability distributions as you like.
- **Service times** are sampled from the custom probability distribution, even though they are placed under the heading :code:`Service_rates`.