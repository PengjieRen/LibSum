# LibSum

1. Decompression. 
  1) Decompress /SRSum.7z to /SRSum
  2) Decompress /root/ROUGE/RELEASE-1.5.5.7z to /root/ROUGE/RELEASE-1.5.5
  3) Decompress /root/model/glove.6B.50d.txt.7z to /root/model/glove.6B.50d.txt
  
2. ROUGE configuration.
  1) Install ActivePerl-5.20.2.2002-MSWin32-x86-64int-299195.msi to C:\Perl\ and make sure C:\Perl\bin\perl.exe exists
  2) Install perl package XML-DOM using cpan with the command: cpan XML::DOM
  
3. Arguments.
  Usage: LibSum.exe [OPTIONS] [trainFilePath] testFilePath

  Options:
    -l, --load=VALUE           Default NULL. Saved model file path (e.g., ./root/model/SRSum.2004.model).
    -q, --qsr=VALUE            Default false. Whether with QSRSum. (for DUC 2005, 2006, and 2007).
    -c, --context=VALUE        Default 4. (The number of contexts in SRSum. Increasing this will get better results but will also slow down the speed).
    -i, --iteration=VALUE      Default 50.
    -t, --threshold=VALUE      Default 0.5.
    -b, --byte=VALUE           Default 665 (DUC 2004 ROUGE settings).
    -w, --word=VALUE           (DUC 2001, 2002 ROUGE settings).
    -h, --help                 Show this message and exit.
  
3. Test existing model.
  For example, test DUC 2004 model: LibSum.exe -l PATH\root\model\SRSum\SRSum.2004.model PATH\root\data\duc2004.test.txt
  The console outputs:
  Intel MKL (x64; revision 11; MKL 2017.0)
  SLF4J: Failed to load class "org.slf4j.impl.StaticLoggerBinder".
  SLF4J: Defaulting to no-operation (NOP) logger implementation
  SLF4J: See http://www.slf4j.org/codes.html#StaticLoggerBinder for further details.
  Reading POS tagger model from edu/stanford/nlp/models/pos-tagger/english-left3words/english-left3words-distsim.tagger ... done [1.0 sec].
  [Read] xxxxxxxxxxxxxxx\root\data\duc2004.test.txt 13300
  Corpus Count: 50
  ..................................................
  [LOG]: DELETE FOLDER ..\root\model\SRSum\rouge-summary__test
  C:\Perl\bin\perl.exe ..\root\Rouge\RELEASE-1.5.5\ROUGE-1.5.5.pl -b 665  -e ..\root\Rouge\RELEASE-1.5.5\data -n 2 -m -2 4 -u -c 95 -x -r 1000 -f A -p 0.5 -t 0 -a -d "..\root\model\SRSum\rouge-summary__test\rouge_config.xml"

  ROURGE_1_R      0.39285
  ROURGE_1_P      0.38792
  ROURGE_1_F      0.39017
  ROURGE_2_R      0.10698
  ROURGE_2_P      0.10572
  ROURGE_2_F      0.1063
  ROURGE_SU4_R    0.14823
  ROURGE_SU4_P    0.14639
  ROURGE_SU4_F    0.14723
  
4. Train new model.
  For example, train DUC 2004 model: LibSum.exe -q false -c 4 -i 100 -t 0.5 -b 665 PATH\root\data\duc2004.train.txt PATH\root\data\duc2004.test.txt
  For example, train DUC 2007 model: LibSum.exe -q true -c 4 -i 100 -t 0.5 -w 250 PATH\root\data\duc2007.train.txt PATH\root\data\duc2007.test.txt
