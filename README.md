# Attach Supp To Main Paper

A Step-by-Step Tutorial for LaTeX with Overleaf.

## Steps

Place before title of `main.tex`.

    \documentclass{article}
    \usepackage{...}

    %%====================================%%
    \usepackage{pdfpages} % include pdfs
    \usepackage{pgffor} % for loops
    
    % Fix for a pdfpages rotation bug with revtex
    \makeatletter
    \AtBeginDocument{\let\LS@rot\@undefined}
    \makeatother
    
    % the name of the supplement PDF file
    \def\supplementfilename{supp.pdf}
    
    % Determine the number of pages of Supp
    \pdfximage{\supplementfilename}
    \def\numbersupplementpages{\the\pdflastximagepages}
    
    \newif\ifarXiv
    \arXivtrue 
    %%====================================%%

    \title{...}
    \begin{document}

Place at the end of the document

    \ifarXiv
        \foreach \x in {1,...,\numbersupplementpages}
        {
            \includepdf[fitpaper=true, pages=\x]{\supplementfilename}
        }
    \fi

    \end{document}

## Usage 
1. Generate `supp.pdf` and Upload to Overleaf Project.
2. Check `main.tex` compiles as expected.
3. Click Submit -> Arxiv in Overleaf.
4. Decompress the .tar file and remove `supp.tex`.
5. Submit to Arxiv