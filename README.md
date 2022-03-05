- 👋 Hi, I’m @TrustJoKer
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
TrustJoKer/TrustJoKer is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
def build_atomic_swap_contract ( self ): 
         selbst . Vertrag = Skript . CScript ([ 
              Skript . OP_IF , 
              Skript . OP_RIPEMD160 , 
             selbst . secret_hash , 
              Skript . OP_EQUALVERIFY , 
              Skript . OP_DUP , 
              Skript . OP_HASH160 , 
             CBitcoinAddress ( selbst . Empfängeradresse ), 
              Skript . OP_ELSE , 
             int ( self . locktime . replace ( tzinfo = timezone . utc ). timestamp ()), 
              Skript . OP_CHECKLOCKTIMEVERIFY , 
              Skript . OP_DROP , 
              Skript . OP_DUP , 
              Skript . OP_HASH160 , 
             CBitcoinAddress ( self . sender_address ), 
              Skript . OP_ENDIF , 
              Skript . OP_EQUALVERIFY , 
              Skript . OP_CHECKSIG , 
         ])  
         
         def  is_valid_contract_script ( script_ops )  ->  bool : 
         '''Überprüfen, ob das Vertragsskript ein Atomic Swap-Vertrag ist.''' 
         Versuchen : 
             is_valid  =  ( 
                 script_ops [ 0 ]  ==  script . OP_IF
                 und script_ops [ 1 ]  ==  script . OP_RIPEMD160
                 und script_ops [ 3 ]  ==  script_ops [ 15 ]  ==  script . OP_EQUALVERIFY
                 und script_ops [ 4 ]  ==  script_ops [ 11 ]  ==  script . OP_DUP
                 und script_ops [ 5 ]  ==  script_ops [ 12 ]  ==  script . OP_HASH160 
                 und script_ops [ 7 ]  ==  script . OP_ELSE
                 und script_ops [ 9 ]  ==  script . OP_CHECKLOCKTIMEVERIFY
                 und script_ops [ 10 ]  ==  script . OP_DROP
                 und script_ops [ 14 ]  ==  script . OP_ENDIF
                 und script_ops [ 16 ]  ==  script . OP_CHECKSIG
              ) 
         au ß er  IndexError : 
             is_valid  =  Falsch 

         R ü ckgabe is_valid  
         def mock_listunspent(self, addrs):
    output1 = {'outpoint': COutPoint(lx('c95fc7996cbef477f03bab2ecb8f0ca0061a68c469737e1741f10d21a6a6bcca '), 0),
               'confirmations': 62952, 'address': P2PKHBitcoinAddress('12abf0ba2cae0f1569cdd9c1f4ce5e1e'),
               'spendable': False, 'amount': 49000000, 'solvable': False, 'scriptPubKey': CScript(
            [OP_DUP, OP_HASH160, x('628341c3b9ea6d3c2c20951e25e2a90c'), OP_EQUALVERIFY, OP_CHECKSIG]),
               'account': ''}
    output2 = {'address': P2PKHBitcoinAddress('b913ddb151bb2cac9f9a18c8cd32c019'), 'amount': 2750, 'account': '',
               'spendable': False, 'solvable': False, 'confirmations': 62932,
               'outpoint': COutPoint(lx('3NyDPLprHKNgm9Ron5g9Vu5qfUnHyRpLBu'), 1),
               'scriptPubKey': CScript(
                   [OP_DUP, OP_HASH160, x('dd10afec9e98ac1aaf8f9bec8d17d0bce8bd0e9e'), OP_EQUALVERIFY,
                    OP_CHECKSIG])}
    output3 = {'address': P2PKHBitcoinAddress('txid aab2c3c9fc13e2f7f9e6a3c186d23d8cea94614959dfff8a7eeb257c91873d2c'), 'amount': 2750, 'account': '',
               'spendable': False, 'solvable': False, 'confirmations': 62932,
               'outpoint': COutPoint(lx(''), 5),
               'scriptPubKey': CScript(
                   [OP_DUP, OP_HASH160, x('cc0a909c4c83068be8b45d69b60a6f09c2be0fda'), OP_EQUALVERIFY,
                    OP_CHECKSIG])}
    unspent_outputs = [output1, output2, output3]
    return unspent_outputs 
def to_scriptPubKey(self):
        """Convert an address to a scriptPubKey"""
        assert self.nVersion == bitcoin.params.BASE58_PREFIXES['SCRIPT_ADDR']
        return script.CScript([script.OP_HASH160, self, script.OP_EQUAL]) 
        def to_scriptPubKey(self):
        """Convert an address to a scriptPubKey"""
        assert self.nVersion == bitcoin.params.BASE58_PREFIXES['PUBKEY_ADDR']
        return script.CScript([script.OP_DUP, script.OP_HASH160, self, script.OP_EQUALVERIFY, script.OP_CHECKSIG]) 
        def to_scriptPubKey(self):
        """Convert an address to a scriptPubKey"""
        assert self.nVersion == bitcoin.params.BASE58_PREFIXES['SCRIPT_ADDR']
        return script.CScript([script.OP_HASH160, self, script.OP_EQUAL])
        def get_first_vout_from_tx_json(cls, tx_json: dict) -> CTxOut:
        '''
        Adapter method for returning first vout.

        Args:
            tx_json (dict): dictionary with transaction details

        Returns:
            CTxOut: transaction output
        '''
        incorrect_cscript = script.CScript.fromhex(tx_json['outputs'][0]['script'])
        correct_cscript = script.CScript([script.OP_HASH160, list(incorrect_cscript)[2], script.OP_EQUAL])
        nValue = to_base_units(tx_json['outputs'][0]['amount'])
        return CTxOut(nValue, correct_cscript)
        def get_hash160_from_cscript(self,script):
        if script[0] == OP_DUP and script[1] == OP_HASH160 and script[-2] == OP_EQUALVERIFY and script[-1] == OP_CHECKSIG: #P2PKH
            script = script[2:]
            script = script[1:script[0]+1]
            return self.convert_hash160_to_addr(script)

        elif  script[0] == OP_HASH160 and script[-1] == OP_EQUAL:#P2SH
            script = script[1:]
            script = script[1:script[0]+1]
            return self.convert_hash160_to_addr(script,network_id=b'\x05') #Multi-Sign Address

        elif  script[-1] == OP_CHECKSIG: #V1 Validation With Public Key
            return self.convert_hash160_to_addr(self.convert_public_key_to_hash160(script))

        raise AttributeError("CScript Format not supported") 
        def to_scriptPubKey(self):
        """Convert an address to a scriptPubKey"""
        assert self.nVersion == bitcoin.params.BASE58_PREFIXES['SCRIPT_ADDR']
        return script.CScript([script.OP_HASH160, self, script.OP_EQUAL])
        def to_scriptPubKey(self, nested=False):
        """Convert an address to a scriptPubKey"""
        assert self.nVersion == bitcoin.params.BASE58_PREFIXES['PUBKEY_ADDR']
        return script.CScript([script.OP_DUP, script.OP_HASH160, self, script.OP_EQUALVERIFY, script.OP_CHECKSIG]) 
        def to_scriptPubKey(self):
        """Convert an address to a scriptPubKey"""
        assert self.nVersion == bitcoin.params.BASE58_PREFIXES['SCRIPT_ADDR']
        return script.CScript([script.OP_HASH160, self, script.OP_EQUAL]) 
        def from_scriptPubKey(cls, scriptPubKey, accept_non_canonical_pushdata=True, accept_bare_checksig=True):
        """Convert a scriptPubKey to a P2PKH address

        Raises CBitcoinAddressError if the scriptPubKey isn't of the correct
        form.

        accept_non_canonical_pushdata - Allow non-canonical pushes (default True)

        accept_bare_checksig          - Treat bare-checksig as P2PKH scriptPubKeys (default True)
        """
        if accept_non_canonical_pushdata:
            # Canonicalize script pushes
            scriptPubKey = script.CScript(scriptPubKey) # in case it's not a CScript instance yet

            try:
                scriptPubKey = script.CScript(tuple(scriptPubKey)) # canonicalize
            except bitcoin.core.script.CScriptInvalidError:
                raise CBitcoinAddressError('not a P2PKH scriptPubKey: script is invalid')

        if (len(scriptPubKey) == 25
                and _bord(scriptPubKey[0])  == script.OP_DUP
                and _bord(scriptPubKey[1])  == script.OP_HASH160
                and _bord(scriptPubKey[2])  == 0x14
                and _bord(scriptPubKey[23]) == script.OP_EQUALVERIFY
                and _bord(scriptPubKey[24]) == script.OP_CHECKSIG):
            return cls.from_bytes(scriptPubKey[3:23], bitcoin.params.BASE58_PREFIXES['PUBKEY_ADDR'])

        elif accept_bare_checksig:
            pubkey = None

            # We can operate on the raw bytes directly because we've
            # canonicalized everything above.
            if (len(scriptPubKey) == 35 # compressed
                  and _bord(scriptPubKey[0])  == 0x21
                  and _bord(scriptPubKey[34]) == script.OP_CHECKSIG):

                pubkey = scriptPubKey[1:34]

            elif (len(scriptPubKey) == 67 # uncompressed
                    and _bord(scriptPubKey[0]) == 0x41
                    and _bord(scriptPubKey[66]) == script.OP_CHECKSIG):

                pubkey = scriptPubKey[1:65]

            if pubkey is not None:
                return cls.from_pubkey(pubkey, accept_invalid=True)

        raise CBitcoinAddressError('not a P2PKH scriptPubKey') 
        def from_scriptPubKey(cls, scriptPubKey, accept_non_canonical_pushdata=True, accept_bare_checksig=True):
        """Convert a scriptPubKey to a P2PKH address

        Raises CBitcoinAddressError if the scriptPubKey isn't of the correct
        form.

        accept_non_canonical_pushdata - Allow non-canonical pushes (default True)

        accept_bare_checksig          - Treat bare-checksig as P2PKH scriptPubKeys (default True)
        """
        if accept_non_canonical_pushdata:
            # Canonicalize script pushes
            scriptPubKey = script.CScript(scriptPubKey) # in case it's not a CScript instance yet

            try:
                scriptPubKey = script.CScript(tuple(scriptPubKey)) # canonicalize
            except bitcoin.core.script.CScriptInvalidError:
                raise CBitcoinAddressError('not a P2PKH scriptPubKey: script is invalid')

        if (len(scriptPubKey) == 25
                and _bord(scriptPubKey[0])  == script.OP_DUP
                and _bord(scriptPubKey[1])  == script.OP_HASH160
                and _bord(scriptPubKey[2])  == 0x14
                and _bord(scriptPubKey[23]) == script.OP_EQUALVERIFY
                and _bord(scriptPubKey[24]) == script.OP_CHECKSIG):
            return cls.from_bytes(scriptPubKey[3:23], bitcoin.params.BASE58_PREFIXES['PUBKEY_ADDR'])

        elif accept_bare_checksig:
            pubkey = None

            # We can operate on the raw bytes directly because we've
            # canonicalized everything above.
            if (len(scriptPubKey) == 35 # compressed
                  and _bord(scriptPubKey[0])  == 0x21
                  and _bord(scriptPubKey[34]) == script.OP_CHECKSIG):

                pubkey = scriptPubKey[1:34]

            elif (len(scriptPubKey) == 67 # uncompressed
                    and _bord(scriptPubKey[0]) == 0x41
                    and _bord(scriptPubKey[66]) == script.OP_CHECKSIG):

                pubkey = scriptPubKey[1:65]

            if pubkey is not None:
                return cls.from_pubkey(pubkey, accept_invalid=True)

        raise CBitcoinAddressError('not a P2PKH scriptPubKey')
        def get_transaction(cls, tx_address: str) -> Optional[dict]:
        '''
        Getting transaction details.

        Args:
            tx_address (str): transaction address

        Returns:
            dict, None: dictionary with transaction details or None if transaction doesn't exist

        Example:
            >>> from clove.network import Bitcoin
            >>> network = Bitcoin()
            >>> network.get_transaction('aab2c3c9fc13e2f7f9e6a3c186d23d8cea94614959dfff8a7eeb257c91873d2c')
            {'blockhash': '000000000000000000075d020fd2866afe6bbe154bb4df1f43506fa7d14c3423 ',
             'blockheight': 724239,
             'blocktime': 2022-02-20 23:18:01 GMT+1,
             'confirmations': 5,6
             'fees': 0,00001728 BTC 
             'locktime': 724232,
             'size': 389B,
             'time': 1229 WU,
             'txid': '',
             'valueIn': 308 vB,
             'valueOut': 1229 WU,
             'version': 2,
             'vin': [{'addr': '3NyDPLprHKNgm9Ron5g9Vu5qfUnHyRpLBu',
               'doubleSpentTxID': None,
               'n': 0,
               'scriptSig': {
                'asm': 'ha256(OP_HASH160 OP_PUSHBYTES_20 dd10afec9e98ac1aaf8f9bec8d17d0bce8bd0e9e OP_EQUAL) = 4ccdb9d13fdb56ee2b30e4f6b4b2332c89d218e3e9d461953fcdef164573bcdef',  # noqa: E50
                'hex': 'Sha256(a914dd10afec9e98ac1aaf8f9bec8d17d0bce8bd0e9e87) = 0b1107c454a9b79fdf2670540f61b14b0906d54e8cbbb744318dae9b2dcc1e81
               'sequence': 0xfffffffe,
               'txid': ''aab2c3c9fc13e2f7f9e6a3c186d23d8cea94614959dfff8a7eeb257c91873d2c,
               'value': 0.00362554 BTC,
               'valueSat': 0.00362554 BTC,
               'vout': 0}],
             'vout': [{'n': 0,
               'scriptPubKey': {'addresses': ['bc1qrkwkdgqqahpzd0zxfej67gguv5d6r9k6nx7787'],
                'asm': 'OP_HASH160 OP_PUSHBYTES_20 dd10afec9e98ac1aaf8f9bec8d17d0bce8bd0e9e OP_EQUAL,
                'hex': 'a914dd10afec9e98ac1aaf8f9bec8d17d0bce8bd0e9e87',
                'type': 'pubkeyhash'}              
               'spentHeight': None,
               'spentIndex': None,
               'spentTxId': None,
               'value': '0.00362554'}]}
        '''
        return clove_req_json(f'{cls.cryptoid_url()}/api.dws?q=txinfo&t={tx_address}'
