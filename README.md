# merge.pl
ORF同定、tRNA同定、16SrRNA同定、rRNA同定の結果から中間結果を生成するスクリプト。
実行にBioPerlが必要であるため、base imageとしてyookuda/bioperlを使用する。

## Usage
```usage
docker run \
    -v data_dir_path:/data \
    --rm \
    $yookuda/merge \
        perl /scripts/merge.pl \
            -f /data/<ゲノムDNA塩基配列のfasta file> \
            -m /data/<MetaGeneAnnotatorの出力ファイル> \
            -t /data/<tRNAscan-SEの出力ファイル> \
            -r /data/<RNAmmerの出力ファイル> \
            -b /data/<16srrna DBでのBLAST検索結果ファイル> \
            -p /data/<output file prefix>
```
- BLAST検索結果ファイルは-outfmt "0" オプションで出力したものを使用する。
- 出力されるファイルは以下の通り。
    - &lt;output file prefix&gt;-na.fasta: 検出されたORFごとの塩基配列のmultiple fasta file
    - &lt;output file prefix&gt;-aa.fasta: 検出されたORFごとのアミノ酸配列のmultiple fasta file
    - &lt;output file prefix&gt;.annt
    - &lt;output file prefix&gt;.csv
    - &lt;output file prefix&gt;.embl
    - &lt;output file prefix&gt;.gbk
    - &lt;output file prefix&gt;.gff
