# Haskell-reddening-code
This is a program which tests 5 colours of a star against progressively reddened standard star colours. It outputs temperature, Av and a Chi^2 value.

In order to provide an estimate of A_{V} and temperature a simple code was written. 

The concept of the code is simple. Contained within is a list of stars of known spectral type. These stars have temperatures ranging from 3050-34,000 K. Along with their temperatures, each of the stars has 5 of its colours within the code, U-B, B-V, V-K, J-H and H-K. The colours of these stars will be referred to as the standard colours. As an input parameter the code takes the same 5 colours, with the associated errors, for the desired test star. These colours will be called the test colours. The actual process of the code is then as follows:

• First the standard colours are compared to the test colours via a \chi^{2}
  test. This is the first step which assumes no reddening. 

• Next the standard colours are reddened slightly. This is carried out by choosing a small A_{V}
  and then calculating A_{\lambda}
  for the other passbands as discussed previously. The 5 colours of each of the standard stars are then changed as is appropriate for this degree of reddening. 

• The new reddened standard colours are then tested against the test colours. 

• Next the standard colours are further reddened and tested until some limiting A_{V}
  is reached. 

The final output of the code is then simply three columns of data: Temperature, A_{V} and a \chi^{2} value. A contour plot of this output reveals the star temperature and V band interstellar extinction level the test colours best correspond to. This code is particularly useful for double checking results. If the interstellar extinction and temperature have been previously calculated using some other method this is a convenient way verify the results.
