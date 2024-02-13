# Lab Report 3

## Part 1 - Bugs
**Failure-inducing input**
```
@Test
public void testReversedFail() {
    int[] input1 = {1, 2, 3, 4, 5};
    assertArrayEquals(new int[]{5, 4, 3, 2, 1}, ArrayExamples.reversed(input1));

    int[] input2 = {1, 1, 2, 2};
    assertArrayEquals(new int[]{2, 2, 1, 1}, ArrayExamples.reversed(input2));
}
```

**Input that doesn't induce failure**
```
@Test
public void testReversedPass() {
    int[] input1 = { };
    assertArrayEquals(new int[]{ }, ArrayExamples.reversed(input1));

    int[] input2 = {0, 0, 0};
    assertArrayEquals(new int[]{0, 0, 0}, ArrayExamples.reversed(input2));
}
```

**The Symptom**
![Image](/images/ArrayExamplesReversedBugSymptom.png) 

**The Bug**  
Before
```
static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
        arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
}
```
After
```
static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
        newArray[i] = arr[arr.length - i - 1];
    }
    return newArray;
}
```

In the original code, the values of the newly created empty array `newArray` were the ones being copied into the original array `arr`. This meant that the original array `arr` got filled with 0's (Java' default intialization value for integers) and the method returned an array of only 0's. To fix this, the order was swapped around so that the values of the original array `arr` became the ones being added to the new empty array `newArray`. Then, after `newArray` is properly filled with the reverse values of `arr`, it gets returned by the method.

## Part 2 - Researching Commands
**-c option**
```
$ grep -c the technical/911report/*.txt
technical/911report/chapter-1.txt:313
technical/911report/chapter-10.txt:336
technical/911report/chapter-11.txt:533
technical/911report/chapter-12.txt:804
technical/911report/chapter-13.1.txt:643
technical/911report/chapter-13.2.txt:467
technical/911report/chapter-13.3.txt:639
technical/911report/chapter-13.4.txt:1070
technical/911report/chapter-13.5.txt:1435
technical/911report/chapter-2.txt:526
technical/911report/chapter-3.txt:1831
technical/911report/chapter-5.txt:635
technical/911report/chapter-6.txt:1046
technical/911report/chapter-7.txt:861
technical/911report/chapter-8.txt:622
technical/911report/chapter-9.txt:1195
technical/911report/preface.txt:68
```
The above command counts how many lines the word "the" (given as the first argument) appears in for each text file in the directory `/technical/911report` (given as the second argument). This can be useful for seeing how many lines refers to a certain word/phrase in set of files.

```
$ grep -c diurnal technical/biomed/1471-2156-2-12.txt
12
```
The above command counts how many lines the word "diurnal" (given as the first argument) appears in for the specified file `technical/biomed/1471-2156-2-12.txt` (given as the second argument). This can be useful for seeing how prevalent a certain idea is in a file without having to look through the whole file yourself.

**-i option**
```
$ grep -i diuRNAL technical/biomed/1471-2156-2-12.txt
          allows detection of diurnal differences
          reported to mask diurnal variation in IOP [ 21 ] ), we
          Diurnal variation in IOP is common in humans and
          underlying the diurnal rhythm are not defined but
          humor drainage may also contribute to diurnal differences
          are needed to define the characteristics of the diurnal
          diurnal rhythms of IOP and that may be relevant to
          diurnal pattern of IOP changes. In agreement with this
          diurnal rhythms compared to pigmented mice [ 75 ] .
          diurnal rhythm of IOP or alters it in different ways
          during the dark. Diurnal rhythms are known to depend on
          diurnal fluctuation of IOP and results in constantly
          the nature of the diurnal rhythm of IOP in the albino B6
        between inbred mouse strains and a diurnal rhythm of IOP
```
The above command finds all lines containing "diurnal"/"DIURNAL" (given as the first argument) regardless of its capitalization in the file `technical/biomed/1471-2156-2-12.txt` (given as the second argument). As seen in the output, there were instances of lines containing "diurnal" or "Diurnal", and by using `-i`, both can be found without having to worry about all possible capitalization combinations of the phrase being searched for.

```
$ grep -i "binge drinking" technical/government/Alcohol_Problems/*.txt
technical/government/Alcohol_Problems/Session2-PDF.txt:drinks/occasion is considered at risk. Binge drinking alone is also
technical/government/Alcohol_Problems/Session2-PDF.txt:identifying patients with binge drinking, we can define binge
technical/government/Alcohol_Problems/Session4-PDF.txt:strategies that are associated with college-based binge drinking is
```
The above command finds all lines containing the phrase "binge drinking" (given as the first argument) regardless of capitalization in all text files of the `/technical/government/Alcohol_Problems` directory (given as the second argument). As the phrase being searched for is longer than it was in the previous example, using `-i` allows us to not worry about even more variation in capitalization while searching for a word or phrase in a set of files.

**-C option**
```
$ grep -C 5 "binge drinking" technical/government/Alcohol_Problems/*.txt
technical/government/Alcohol_Problems/Session2-PDF.txt-point." A cut point with a high sensitivity and specificity should
technical/government/Alcohol_Problems/Session2-PDF.txt-be manifest in an ideal test.
technical/government/Alcohol_Problems/Session2-PDF.txt-Theoretically, an ideal test should remain accurate throughout
technical/government/Alcohol_Problems/Session2-PDF.txt-the alcohol use spectrum. However, real tests don't perform
technical/government/Alcohol_Problems/Session2-PDF.txt-uniformly across a spectrum. For example, if we're interested in
technical/government/Alcohol_Problems/Session2-PDF.txt:identifying patients with binge drinking, we can define binge
technical/government/Alcohol_Problems/Session2-PDF.txt-drinking as 3, 4, 5, or 6 drinks on an occasion. Screening tests
technical/government/Alcohol_Problems/Session2-PDF.txt-designed for patients with more severe problems (6 drinks) will be
technical/government/Alcohol_Problems/Session2-PDF.txt-less sensitive at identifying patients with less severe problems (3
technical/government/Alcohol_Problems/Session2-PDF.txt-drinks).
technical/government/Alcohol_Problems/Session2-PDF.txt-An ideal test would perform uniformly in all populations and
--
technical/government/Alcohol_Problems/Session4-PDF.txt-agent/vehicle of morbidity and mortality, alcohol, and the
technical/government/Alcohol_Problems/Session4-PDF.txt-environment in which these groups interface with alcohol.
technical/government/Alcohol_Problems/Session4-PDF.txt-Policy-relevant studies are needed to address the marketing,
technical/government/Alcohol_Problems/Session4-PDF.txt-distribution, and sale of alcohol to high-risk groups and
technical/government/Alcohol_Problems/Session4-PDF.txt-environments. Research that examines pricing schemes and marketing
technical/government/Alcohol_Problems/Session4-PDF.txt:strategies that are associated with college-based binge drinking is
technical/government/Alcohol_Problems/Session4-PDF.txt-needed. A set of single policy-relevant questions should be
technical/government/Alcohol_Problems/Session4-PDF.txt-routinely asked such as, "Where did you buy the alcohol?" and
technical/government/Alcohol_Problems/Session4-PDF.txt-"Where were you drinking before you were injured?" Linking the
technical/government/Alcohol_Problems/Session4-PDF.txt-abuse/individual behavior questions to when and where the alcohol
technical/government/Alcohol_Problems/Session4-PDF.txt-was consumed has important implications. Research that evaluates
```
The above command locates lines containing "binge drinking" in all text files in the directory `/technical/government/Alcohol_Problems`, then prints out the line and 5 lines before and after it. This can be useful if you want to read a bit about how the file is using a specific word or phrase, and in this case, we can see more of what the two files say about binge drinking.

```
$ grep -C 3 "deubiquitinating enzymes" technical/plos/journal.pbio.0020013.txt
        proteins rarely accumulate in the cytoplasm of “healthy” cells, as they are either
        irreversibly degraded or deubiquitinated and rescued. It is thought that this competition
        provides a certain level of stringency or quality control to the system. Based on sequence
        homology, deubiquitinating enzymes were traditionally classified into two families:
        ubiquitin-specific proteases (UBPs or USPs) and ubiquitin carboxy-terminal hydrolases
        (UCHs). Both enzyme families are classified as cysteine proteases that employ an active
        site thiol to cleave ubiquitin from its target (Kim et al. 2003; Wing 2003).
--
        + /JAMM sequence. The fourth ligand appears to be a water molecule
        activated through interactions with the conserved glutamate to serve as the active site
        nucleophile. Overall, this protein certainly has properties consistent with a
        metallohydrolase and can serve as the prototype for the deubiquitinating enzymes in its
        class. This revelation adds an all-new enzymatic activity and, with it, an additional layer
        of regulation to the ubiquitin–proteasome system.
        Now that it is evident that the proteasome contains a member of a novel metalloprotease
        family, a fundamental question can be raised: why does a proteolytic enzyme like the
        proteasome need auxiliary proteases for hydrolysis of ubiquitin domains? At first glance,
        the delegation of tasks between the proteolytic subunits of the proteasome (situated in the
        proteolytic core particle) and the auxiliary deubiquitinating enzymes (situated in the
        regulatory particle) is clear-cut: the latter cleave between ubiquitin domains, while the
        core proteolytic subunits process the target protein itself (Figure 1). However, this still
        does not explain the mechanistic rational for finding deubiquitination within the
--
        Once bound to the proteasome, a polyubiquitinated substrate can be unfolded by the RP
        and irreversibly translocated into the CP. It has been proposed that long polyubiquitin
        chains commit a substrate to unfolding and degradation by the proteasome, whereas short
        chains are poor substrates because they are edited by deubiquitinating enzymes, resulting
        in premature substrate release (Eytan et al. 1993; Lam et al. 1997; Thrower et al. 2000;
        Guterman and Glickman 2003). Extended polyubiquitin chains could slow down chain
        disassembly, thereby allowing ample time for unfolding and proteolysis of the substrate
        (Figure 2). Interestingly, both “trimming” and “shaving” deubiquitinating activities are
        associated with the proteasome, though the exact contribution of the various
        proteasome-associated deubiquitinating enzymes to each of these distinct activities has yet
        to be elucidated. It is expected that in order to obtain efficient proteolysis of the
        target, shaving of chains at their proximal ubiquitin should be slower than the rate of
        trimming at the distal moiety. As an outcome of this requirement, longer polyubiquitin tags
```
The above command locates lines containing "deubiquitinating enzymes" in the text file `/technical/plos/journal.pbio.0020013.txt`, then prints out each line along with 3 lines before and after it, grouping sections into one if they overlap. This can be useful for better understanding how a word or phrase fits into the larger picture a file, instead of being limited to seeing just the line the word or phrase is found on.

**-l option**
```
$ grep -l "health" technical/biomed/gb*.txt
technical/biomed/gb-2003-4-1-r7.txt
technical/biomed/gb-2003-4-3-r17.txt
technical/biomed/gb-2003-4-4-r24.txt
technical/biomed/gb-2003-4-7-r46.txt
```
The above command prints out the names of all the "gb" text files located in the directory `/technical/biomed` that exactly contains the word "health". This can be useful when you're just looking for the files in a set of files that contain a specific word or phrase, and don't need to the see the actual line with the word or phrase.

```
$ grep -l "legal rights" technical/government/Media/*.txt
technical/government/Media/Too_Crucial_to_Take_Cut.txt
technical/government/Media/Unusual_Woodburn.txt
technical/government/Media/Weak_economy.txt
```
The above command prints out the names of all the text files located in the directory `/technical/government/Media` that exactly contains the phrase "legal rights". This can be useful for searching for files that contain a word or phrase without worrying about the lines that the word or phrase is located on.

**Source for finding grep options**

Source: [https://www.geeksforgeeks.org/grep-command-in-unixlinux/](https://www.geeksforgeeks.org/grep-command-in-unixlinux/)
