<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>IQ-TREE Phylogenetic Analysis Tutorial</title>
</head>
<body>

<h1>IQ-TREE Phylogenetic Analysis Tutorial: Orthopoxvirus Species</h1>

<h2>1. Introduction</h2>
<p>In this exercise, we will work with the complete genomes of 13 Orthopoxvirus species, comparing different strategies for phylogenetic inference using IQ-TREE. The dataset includes protein alignments across species with 100% coverage in all sequences. Our goal is to explore the impact of using a single substitution model, a partitioned model, and a merged model approach on the robustness of our phylogenetic hypothesis.</p>

<h3>Species and Accession Numbers</h3>
<table>
  <tr>
    <th>Species</th>
    <th>Accession Number</th>
  </tr>
  <tr><td>Buffalopox</td><td>DQ439815</td></tr>
  <tr><td>Camelpox</td><td>DQ792504</td></tr>
  <tr><td>Ectromelia</td><td>JQ410350</td></tr>
  <tr><td>Horsepox</td><td>LR800244</td></tr>
  <tr><td>Orthopoxvirus</td><td>MF477237</td></tr>
  <tr><td>Raccoonpox</td><td>MH816996</td></tr>
  <tr><td>Skunkpox</td><td>MK910851</td></tr>
  <tr><td>Taterapox</td><td>MW883892</td></tr>
  <tr><td>Vaccinia</td><td>NC_008291</td></tr>
  <tr><td>Vaccinia</td><td>NC_027213</td></tr>
  <tr><td>Variola</td><td>NC_031033</td></tr>
  <tr><td>Volepox</td><td>NC_031038</td></tr>
</table>

<p>After downloading these genomes, we extracted 53 proteins with 100% coverage across all species, creating individual protein alignments with MAFFT and a concatenated alignment for IQ-TREE analyses.</p>

<h2>2. Diversity of Substitution Models and Choosing the Optimal Model</h2>

<h3>DNA vs. Protein Models</h3>
<p>In phylogenetics, substitution models describe the probability of mutations occurring at different sites in the sequence. DNA models (like GTR and HKY) consider nucleotide substitutions, while protein models (like JTT and LG) account for amino acid replacements.</p>

<h3>Choosing the Optimal Model</h3>
<p>IQ-TREE's ModelFinder enables automatic model selection by testing various models and calculating which one best fits the data using criteria like AIC or BIC. This tutorial includes examples of running ModelFinder for both DNA and protein sequences.</p>

<h2>3. Exercise Overview</h2>

<p>We'll use IQ-TREE to analyze the concatenated protein alignments under three approaches:</p>
<ol>
  <li><strong>Single Substitution Model</strong>: Applies one substitution model to all sequences.</li>
  <li><strong>Partitioned Model</strong>: Uses the best model for each partition (protein) individually.</li>
  <li><strong>Merged Model (MFP+MERGE)</strong>: Merges partitions to find an optimal model fit.</li>
</ol>

<h2>4. IQ-TREE Commands and Analysis Steps</h2>

<h3>Step 1: Running IQ-TREE with a Single Substitution Model</h3>
<pre><code>iqtree -s concatenated_proteins.phy -m LG+G -B 1000</code></pre>
<p>Explanation: This command specifies the LG model with gamma rate variation (+G) and performs ultrafast bootstrapping (-B 1000) for branch support.</p>

<h3>Step 2: Running IQ-TREE with Partitioned Model Using ModelFinder</h3>
<pre><code>iqtree -s concatenated_proteins.phy -p proteins_partitions.nex -m MFP -B 1000</code></pre>
<p>Explanation: This command applies ModelFinder (-m MFP) to identify the best model for each partition (protein). Bootstrapping is performed with 1000 replicates.</p>

<h3>Step 3: Using the Merged Model with ModelFinder (MFP+MERGE)</h3>
<pre><code>iqtree -s concatenated_proteins.phy -p proteins_partitions.nex -m MFP+MERGE -B 1000</code></pre>
<p>Explanation: Here, IQ-TREE merges similar partitions based on model fit (MFP+MERGE), creating a balanced approach between single and fully partitioned models.</p>

<h3>Step 4: Resampling Strategies</h3>
<ol>
  <li><strong>Bootstrap by Gene</strong>:
    <pre><code>iqtree -s concatenated_proteins.phy -p proteins_partitions.nex -B 1000 --sampling GENE</code></pre>
  </li>
  <li><strong>Bootstrap by Gene and Site</strong>:
    <pre><code>iqtree -s concatenated_proteins.phy -p proteins_partitions.nex -B 1000 --sampling GENESITE</code></pre>
  </li>
</ol>
<p>Explanation: These options provide additional control over how bootstrap samples are generated, potentially enhancing support values by reducing false positives.</p>

<h2>5. Results Interpretation and Comparison</h2>
<ol>
  <li><strong>Single Model vs. Partitioned Models</strong>: Compare how branch supports and tree topology differ between single model and partitioned model approaches.</li>
  <li><strong>MFP+MERGE Strategy</strong>: Assess whether merging improves computational efficiency without sacrificing tree support or topology.</li>
  <li><strong>Bootstrap Sampling</strong>: Evaluate whether resampling by gene or gene and site leads to improved support values.</li>
</ol>

<h2>6. Additional Topic Focus: ModelFinder and Partition Merging</h2>
<p>In this exercise, we focus on <strong>partition merging with ModelFinder</strong> to optimize tree topology. By using the MFP+MERGE option, we test if merging similar partitions maintains phylogenetic resolution while reducing the computational burden. This exercise highlights when and why partition merging can be advantageous in multi-protein datasets.</p>

<h2>7. Resources and Suggested Readings</h2>
<ol>
  <li><strong>ModelFinder</strong>: Lanfear et al., 2012 – For details on model selection and partition merging in phylogenetics.</li>
  <li><strong>Bootstrap Resampling</strong>: Nei et al., 2001; Seo et al., 2005 – For insights on resampling strategies in phylogenetic analysis.</li>
</ol>

<h2>Slides Overview</h2>
<ol>
  <li>Slide 1: Introduction to Orthopoxvirus Phylogenetic Analysis</li>
  <li>Slide 2: Substitution Models (DNA vs. Protein)</li>
  <li>Slide 3: Model Selection in IQ-TREE (ModelFinder)</li>
  <li>Slide 4: IQ-TREE Commands and Partition Strategies</li>
  <li>Slide 5: Results Interpretation</li>
</ol>

</body>
</html>
