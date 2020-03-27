  
{
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# **FUZZY CALCULATOR PROGRAM**"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# 1. Fuzzy Set Operators"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## - Transpose"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 1,
   "metadata": {},
   "outputs": [],
   "source": [
    "def trans(x: list):\n",
    "    data = []\n",
    "    for i in range(len(x[0])):\n",
    "        temp = []\n",
    "        for j in range(len(x)):\n",
    "            temp.append(x[j][i])\n",
    "        data.append(temp)\n",
    "    return data"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## - S-Norm"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 2,
   "metadata": {},
   "outputs": [],
   "source": [
    "def s_norm(x, y):\n",
    "    if isinstance(x, list) and isinstance(y, list):\n",
    "        if isinstance(x[0], list) and isinstance(y[0], list):\n",
    "            return [[x[i][j]+y[i][j]-x[i][j]*y[i][j] for j in range(len(x[0]))] for i in range(len(x))]\n",
    "        else: \n",
    "            return [x[i]+y[i]-x[i]*y[i] for i in range(len(x))] \n",
    "    else:\n",
    "        return x+y-x*y # algebraic sum"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## - T-Norm"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "metadata": {},
   "outputs": [],
   "source": [
    "def t_norm(x: list, y: list):\n",
    "    if isinstance(x, list) and isinstance(y, list):\n",
    "        if isinstance(x[0], list) and isinstance(y[0], list):\n",
    "            return [[x[i][j]*y[i][j] for j in range(len(x[0]))] for i in range(len(x))]\n",
    "        else: \n",
    "            return [x[i]*y[i] for i in range(len(x))]\n",
    "    else:\n",
    "        return x*y"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## - C-Std"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "metadata": {},
   "outputs": [],
   "source": [
    "def c_std(x: list):\n",
    "    if isinstance(x, list):\n",
    "        if isinstance(x[0], list):\n",
    "            return [[1-x[i][j] for j in range(len(x[0]))] for i in range(len(x))]\n",
    "        else: \n",
    "            return [1-x[i] for i in range(len(x))]\n",
    "    else:\n",
    "        return 1-x"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# 2. Fuzzy Relation"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## - S-Norm Relation"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
   "metadata": {},
   "outputs": [],
   "source": [
    "def s_norm_relation(x: list, y: list):\n",
    "    data = []\n",
    "    for i in range(len(x)):\n",
    "        temp = []\n",
    "        for j in range(len(y)):\n",
    "            temp.append(s_norm(x[i], y[j]))\n",
    "        data.append(temp)\n",
    "    return data"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## - T-Norm Relation"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 6,
   "metadata": {},
   "outputs": [],
   "source": [
    "def t_norm_relation(x: list, y: list):\n",
    "    data = []\n",
    "    for i in range(len(x)):\n",
    "        temp = []\n",
    "        for j in range(len(y)):\n",
    "            temp.append(t_norm(x[i], y[j]))\n",
    "        data.append(temp)\n",
    "    return data"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## - Composition"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 7,
   "metadata": {},
   "outputs": [],
   "source": [
    "def composition(x: list, y:list):\n",
    "    if len(x) == len(y[0]) and len(y) == len(x[0]):\n",
    "        data = []\n",
    "        for i in range(len(x)):\n",
    "            temp = []\n",
    "            for j in range(len(x)):\n",
    "                a = x[i]\n",
    "                b = [y[t][j] for t in range(len(y))]\n",
    "                temp.append(max([a[t]*b[t] for t in range(len(y))]))\n",
    "            data.append(temp)\n",
    "        return data\n",
    "    else:\n",
    "        return 0"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# 3.Linguistic Operators"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## - Hedges"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 8,
   "metadata": {},
   "outputs": [],
   "source": [
    "def rather(u):\n",
    "    if isinstance(u, list):\n",
    "        if isinstance(u[0], list):\n",
    "            return [[u[i][j]**0.5 for j in range(len(u[0]))] for i in range(len(u))]\n",
    "        else:\n",
    "            return [u[i]**0.5 for i in range(len(u))]\n",
    "    else:        \n",
    "        return u**0.5\n",
    "\n",
    "def very(u):\n",
    "    if isinstance(u, list):\n",
    "        if isinstance(u[0], list):\n",
    "            return [[u[i][j]**2 for j in range(len(u[0]))] for i in range(len(u))]\n",
    "        else:\n",
    "            return [u[i]**2 for i in range(len(u))]\n",
    "    else:        \n",
    "        return u**2"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# Examples"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## - Fuzzy Set Operators"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### C-Std, S-Norm, and T-Norm"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 9,
   "metadata": {},
   "outputs": [],
   "source": [
    "A = [ 0, 0.1, 0.3, 0.5, 0.6, 0.8]\n",
    "B = [ 0.8, 1, 0.9, 0.7, 0.5, 0.3]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 10,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[1, 0.9, 0.7, 0.5, 0.4, 0.19999999999999996]"
      ]
     },
     "execution_count": 10,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "c_std(A)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 11,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[0.19999999999999996, 0, 0.09999999999999998, 0.30000000000000004, 0.5, 0.7]"
      ]
     },
     "execution_count": 11,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "c_std(B)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 12,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[0.8, 1.0, 0.9299999999999999, 0.85, 0.8, 0.8600000000000001]"
      ]
     },
     "execution_count": 12,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "s_norm(A,B)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 13,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[0.0, 0.1, 0.27, 0.35, 0.3, 0.24]"
      ]
     },
     "execution_count": 13,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "t_norm(A,B)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## - Fuzzy Relation"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 14,
   "metadata": {},
   "outputs": [],
   "source": [
    "A = [0, 0.3, 0.5, 0.7, 0.9, 1]\n",
    "B = [0.8, 0.5, 0.1, 0.3]\n",
    "C = [[1.00, 0.80, 0.60, 0.40, 0.20, 0.00],\n",
    "     [0.8, 1, 0.8, 0.6, 0.4, 0.2],\n",
    "     [0.6, 0.8, 1, 0.8, 0.6, 0.4],\n",
    "     [0.4, 0.6, 0.8, 1, 0.8, 0,6]]\n",
    "R = [[i+j-i*j for j in B] for i in A]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 15,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[[0.8, 0.5, 0.1, 0.3],\n",
       " [0.8600000000000001, 0.65, 0.37, 0.51],\n",
       " [0.9, 0.75, 0.5499999999999999, 0.65],\n",
       " [0.9400000000000001, 0.85, 0.73, 0.79],\n",
       " [0.9800000000000001, 0.95, 0.91, 0.9299999999999999],\n",
       " [1.0, 1.0, 1.0, 1.0]]"
      ]
     },
     "execution_count": 15,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "R"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### 1. CoR (C composition R)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 16,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[[0.8, 0.52, 0.32999999999999996, 0.40800000000000003],\n",
       " [0.8600000000000001, 0.65, 0.43999999999999995, 0.52],\n",
       " [0.9, 0.75, 0.584, 0.65],\n",
       " [0.9400000000000001, 0.85, 0.73, 0.79]]"
      ]
     },
     "execution_count": 16,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "composition(C,R)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### 2. RoC (R composition C)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 17,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[[0.8, 0.6400000000000001, 0.48, 0.32000000000000006, 0.24, 0.1],\n",
       " [0.8600000000000001,\n",
       "  0.6880000000000002,\n",
       "  0.52,\n",
       "  0.51,\n",
       "  0.40800000000000003,\n",
       "  0.148],\n",
       " [0.9, 0.75, 0.6000000000000001, 0.65, 0.52, 0.21999999999999997],\n",
       " [0.9400000000000001, 0.85, 0.73, 0.79, 0.6320000000000001, 0.292],\n",
       " [0.9800000000000001,\n",
       "  0.95,\n",
       "  0.91,\n",
       "  0.9299999999999999,\n",
       "  0.744,\n",
       "  0.36400000000000005],\n",
       " [1.0, 1.0, 1.0, 1.0, 0.8, 0.4]]"
      ]
     },
     "execution_count": 17,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "composition(R,C)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## 3. R transpose"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 18,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[[0.8, 0.8600000000000001, 0.9, 0.9400000000000001, 0.9800000000000001, 1.0],\n",
       " [0.5, 0.65, 0.75, 0.85, 0.95, 1.0],\n",
       " [0.1, 0.37, 0.5499999999999999, 0.73, 0.91, 1.0],\n",
       " [0.3, 0.51, 0.65, 0.79, 0.9299999999999999, 1.0]]"
      ]
     },
     "execution_count": 18,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "R_trans = trans(R)\n",
    "R_trans"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### 2. RoR_transpose (R composition R_transpose)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 19,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[[0.6400000000000001,\n",
       "  0.6880000000000002,\n",
       "  0.7200000000000001,\n",
       "  0.7520000000000001,\n",
       "  0.7840000000000001,\n",
       "  0.8],\n",
       " [0.6880000000000002,\n",
       "  0.7396000000000001,\n",
       "  0.7740000000000001,\n",
       "  0.8084000000000001,\n",
       "  0.8428000000000002,\n",
       "  0.8600000000000001],\n",
       " [0.7200000000000001,\n",
       "  0.7740000000000001,\n",
       "  0.81,\n",
       "  0.8460000000000001,\n",
       "  0.8820000000000001,\n",
       "  0.9],\n",
       " [0.7520000000000001,\n",
       "  0.8084000000000001,\n",
       "  0.8460000000000001,\n",
       "  0.8836000000000002,\n",
       "  0.9212000000000001,\n",
       "  0.9400000000000001],\n",
       " [0.7840000000000001,\n",
       "  0.8428000000000002,\n",
       "  0.8820000000000001,\n",
       "  0.9212000000000001,\n",
       "  0.9604000000000001,\n",
       "  0.9800000000000001],\n",
       " [0.8, 0.8600000000000001, 0.9, 0.9400000000000001, 0.9800000000000001, 1.0]]"
      ]
     },
     "execution_count": 19,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "composition(R, R_trans)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## - Linguistic Operators"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 20,
   "metadata": {},
   "outputs": [],
   "source": [
    "A = [ 0, 0.1, 0.3, 0.5, 0.6, 0.8]\n",
    "B = [ 0.8, 1, 0.9, 0.7, 0.5, 0.3]"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### 1. Not A"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 21,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[1, 0.9, 0.7, 0.5, 0.4, 0.19999999999999996]"
      ]
     },
     "execution_count": 21,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "not_A = c_std(A)\n",
    "not_A"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### 2. Very A"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 22,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[0, 0.010000000000000002, 0.09, 0.25, 0.36, 0.6400000000000001]"
      ]
     },
     "execution_count": 22,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "very_A = very(A)\n",
    "very_A"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### 3. Rather A"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 23,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[0.0,\n",
       " 0.31622776601683794,\n",
       " 0.5477225575051661,\n",
       " 0.7071067811865476,\n",
       " 0.7745966692414834,\n",
       " 0.8944271909999159]"
      ]
     },
     "execution_count": 23,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "rather_A = rather(A)\n",
    "rather_A"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### 4. Not A AND B"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 24,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[0.8, 0.9, 0.63, 0.35, 0.2, 0.059999999999999984]"
      ]
     },
     "execution_count": 24,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "t_norm(not_A, B)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### 5. Very Not A"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 25,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[1, 0.81, 0.48999999999999994, 0.25, 0.16000000000000003, 0.03999999999999998]"
      ]
     },
     "execution_count": 25,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "very(not_A)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### 6. Not B"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 26,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[0.19999999999999996, 0, 0.09999999999999998, 0.30000000000000004, 0.5, 0.7]"
      ]
     },
     "execution_count": 26,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "not_B = c_std(B) \n",
    "not_B"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### 7. Rather Not B"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 28,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[0.44721359549995787,\n",
       " 0.0,\n",
       " 0.3162277660168379,\n",
       " 0.5477225575051662,\n",
       " 0.7071067811865476,\n",
       " 0.8366600265340756]"
      ]
     },
     "execution_count": 28,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "rather(not_B)"
   ]
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.6.9"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 4
}