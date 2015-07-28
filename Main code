import System.IO
import Data.List
import System.Directory
import Spectraltypes



{- So we import the spectraltypes from the module SpectralTypes. 
Each of these is just a list with 6 parameters, 5 colours and a temp.
 
For clarity, in the 'main' section of the code, we map over the list allspectra. 
This is just a list of lists, where each sublist is a spectraltype as mentioned above. 

The Reddener function just takes a spectraltype and an Av and reddens the colours (leaving the temp alone).

The Chisquared function takes a list of tuples (in this case NVSS with colours and errors), and a spectral type. 
It returns a number which is a chisquared test.
The chitest function takes a spectraltype. It then creates a list of reddened spectraltypes for each Av in the list avlist 
(we have a list of lists, where each sublist is a spectraltype reddened to a certain degree. 
Then what it does is perform a chisquared analysis of each of the reddened spectral types. 
This is its output - a list of chisquared values. 

The output function takes a stellartype as a parameter. What is does is basically perform the chitest function, 
but zip the chisquared output values with their associated temperature and Av values. By mapping this function over 
a list of stellartypes we get our desired output for a contour plot (but we must be sure to flatten the list). 
So our output from this program is 3 columns,
(1)  Temperature
(2)  Av
(3)  Chisquared


If you would like to use the code yourself, just make sure that the Spectraltypes.hs file is in the same folder. 
You can then enter the colours and errors of your star of interest in the nvss list ( it has form U-B, B-V, V-K, J-H, H-K ). 
 You can also change the values of Av by playing with the avlist. -}






reddener :: (Real a, Floating a) => [a] -> a -> [a]
reddener [ a, b, c, d, e, f] av = [ a + av*(0.207), b + av*(0.324), c + av*(0.888), d + av*(0.107), e + av*(0.053), f]



chisquared :: (Real a, Floating a) => [(a,a)] -> [a] -> a
chisquared [(a1,e1),(a2,e2),(a3,e3),(a4,e4),(a5,e5)] [x,y,z,f,g,_] = ((a1-x)**2)/((e1)**2) + ((a2-y)**2)/((e2)**2) + ((a3-z)**2)/((e3)**2) + ((a4-f)**2)/((e4)**2) + ((a5-g)**2)/((e5)**2)	


chitest :: [Double] -> [Double]	
chitest starcolours = map (chisquared scalednvss) (map (reddener starcolours) avlist)


output :: [Double] -> [[Char]]
output starcolours = zipWith3 (\x y z -> show x ++ "\t\t" ++ show y ++ "\t\t" ++ show z) (replicate (length avlist) (last starcolours)) avlist (chitest starcolours)  ++ [""]


nvss = [(-0.14,0.107),(0.67,0.085),(3.13,0.072),(0.458,0.084),(0.551,0.086)]
scalednvss = [(-0.14,0.453),(0.67,0.360),(3.13,0.305),(0.458,0.356),(0.551,0.364)]  -- errors scaled for chi^2 of 3
spica = [(0.54,0.02),(-0.23,0.02),(-0.67,0.02),(-0.04,0.02),(-0.1,0.02)]
avlist = 0:[0.1,0.3..6]

main = do let results = concat $ map output allspectra
       handle <- openFile "beta.dat" WriteMode
       mapM_ (hPutStrLn handle) results
       hClose handle







